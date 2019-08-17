---
layout: post
title: An introduction to Nancy
date: '2016-06-12 19:56:17'
tags:
- development
- asp-net
- c
- mvc
---

If you haven't heard of [Nancy](http://nancyfx.org) before, is it described as

> ...a lightweight, low-ceremony, framework for building HTTP based services on .Net and Mono. The goal of the framework is to stay out of the way as much as possible and provide a super-duper-happy-path to all interactions.

Think of Nancy as ASP.NET MVC or Web API after going on a diet. A long, hard and life-changing diet.

Setup takes minutes, documentation is clear and precise, and there is almost no boiler-plate code to write to get things up and running. You can seriously put together a HTTP based service in minutes.

That's enough of the sales pitch and time to get on with the important stuff.

In my last post I covered an issue we found with some old code that was tightly coupled to a database and needed a bit of an overhaul. What we needed to do was move some business logic out of a widely-deployed add-in to our ERP package, and move it to a central service for ease of maintenance.

The thought of setting up a site using ASP.NET MVC or ASP.NET Web API had me shudder because the code for this service would be eclipsed by the amount of setup, configuration settings and plumbing these frameworks need. I needed something quicker and easier, and that's when I remembered a framework called [Nancy](http://nancyfx.org) mentioned on a recent podcast I had heard.

So I scanned over the [documentation](https://github.com/NancyFx/Nancy/wiki/Documentation) and chose to implement Nancy by [self-hosting](https://github.com/NancyFx/Nancy/wiki/Self-Hosting-Nancy) it inside of a Windows Service. No IIS needed, and it keeps this service small and relatively portable.

I won't go in to the ins-and-outs of creating a Windows Service as that is outside of the scope of this post, but you'll find plenty of guidance online if you search for it.

At the heart of a Nancy application are modules. These define the behavior of your application and can be compared to a Controller/ApiController in the ASP.NET frameworks.

Here's an overview of our Nancy module:

```language-csharp,line-numbers,theme
public class PaymentOnAccountModule : NancyModule
{
    public PaymentOnAccountModule()
    {
        Get["/payment-on-account"] = _ => "We don't accept GET requests - go away";

        Post["/payment-on-account"] = _ =>
        {
            var model = this.Bind<PaymentOnAccountModel>();

            //Connect to the database
            //Perform update
            //Run other business logic

            if (everythingWasOkay)
            {
                return HttpStatusCode.OK;
            }
            else
            {
                return HttpStatusCode.BadRequest;
            }
        };
    }
}
```

In its simplest form, a module is no more than a class inheriting from NancyModule, and defining the routes and actions in the constructor.

The first line of the constructor defines what happens if someone performs a GET request to /payment-on-account. This service doesn't need to return anything so we show the client a simple message.

The Post line is where the work happens. We start by using the [model-binding functionality](https://github.com/NancyFx/Nancy/wiki/Model-binding) built-in to Nancy to bind the POSTed data in to a concrete ```PaymentOnAccountModel``` which is no different to a [POCO](https://en.wikipedia.org/wiki/Plain_Old_CLR_Object) you would write for ASP.NET MVC or Web API. This allows us to access the submitted data in a strongly-typed manner.

After doing our work, we need to respond to the client with the result. We keep it simple by returning either a 200 or 400 HTTP status code as an indication of success or failure.

So that's our module, but how do we make use of it?

Inside of the Service class for our Windows Service (the host application for Nancy in this case), we define the host at the class level:

```language-csharp,line-numbers,theme
NancyHost host;
```

Inside of the constructor we use:

```language-csharp,line-numbers,theme
var port = MyService.Properties.Settings.Default.HTTPPort;
StaticConfiguration.DisableErrorTraces = false;
var hostConfiguration = new HostConfiguration
{
    UrlReservations = new UrlReservations() { CreateAutomatically = true }
};

host = new NancyHost(hostConfiguration, GetUriParams(port));
```

As we already know hard-coding is bad, we define the HTTP port Nancy will use in a configuration file and load this to start with.

Next we define the configuration we want Nancy to use by creating a ```HostConfiguration``` object. ```UrlReservations = new UrlReservations() { CreateAutomatically = true }``` instructs Nancy to register the URLs with Windows automatically so you don't need to set these up manually. This action requires administrative rights at runtime, but as we're running as a Windows Service we can cover this requirement easier than if this was an application running in user space.

Finally we create an instance of ```NancyHost```, passing it the previously discussed host configuration, and a list of the URLs to listen on. ```GetUriParams``` is nothing special and simply builds a list of URIs that we want Nancy to listen on based on the machines hostname and IP addresses. If you're testing this yourself, you can use a URL to listed on "http://localhost:port" to start with.

As it stands, everything we need is setup but Nancy won't respond just yet. We need to inform Nancy to start and the local place to do this is in the OnStart event of the Windows Service:

```language-csharp,line-numbers,theme
protected override void OnStart(string[] args)
{
    host.Start();
}
```

We will also stop Nancy if the service is stopped:

```language-csharp,line-numbers,theme
protected override void OnStop()
{
    host.Stop();
}
```

As soon as the Windows starts this service, Nancy will be ready and listening.

Notice we haven't had to do any real configuration for Nancy. We haven't had to teach it about our module, wire the module up in a config file or anything. Nancy is smart enough to find the module based on the class inheriting from ```NancyModule```.

Other than using Attribute Routing, ASP.NET MVC/Web API can't come close to this level of simplicity! Our of the box, Nancy will even respond with its own little 404 error page should a client get a URL wrong.

Back to our situation, once we followed the steps above we had a working API service wrapped in a Windows Service.

Dropped on to its final home in production it has been running perfectly for a week now and memory usage is a tiny 8MB so it isn't going to hog resources at all.

I've only touched on the absolute basics of Nancy here but it's all we needed. I will certainly consider Nancy in future when we need a HTTP service, especially for these microservice like applications.

For more information, go and check out the [Nancy](http://nancyfx.org) website, or the project over on [GitHub](https://github.com/NancyFx/Nancy).