---
layout: post
title: Visual Studio Application Insights - An overview
date: '2016-08-08 19:32:11'
tags:
- development
- it
- devops
- application-insights
---

Have you heard of [Application Insights](https://www.visualstudio.com/products/application-insights-vs)? It's a great tool to give you a precise look at the activity and issues in your web apps and services. After setting it up, you can use it to detect, analyse and organise the client and server-side of your application.

Application Insights is performance monitoring, analytics, logging, exception handling, and more on steroids. When talking about web apps, Application Insights gives you an immense amount of detail for every request to your site to you can learn what your visitors are doing, and the experience they are receiving.

<center>
<iframe width="853" height="480" src="https://www.youtube.com/embed/fX2NtGrh-Y0?rel=0" frameborder="0" allowfullscreen></iframe>
</center>

Don't be put off by this being a Microsoft product though. In true new-Microsoft style, Application Insights works with [any platform and any language](https://azure.microsoft.com/en-gb/documentation/articles/app-insights-platforms/). While I'm sure there are some obscure platforms or languages you may have to roll your own integration with, [Microsoft have covered almost all of the key options](https://azure.microsoft.com/en-gb/documentation/articles/app-insights-platforms/) out of the box. It goes without saying that Visual Studio users get the first-class experience, but it won't take you long to get up and running regardless of the technology you use, or the provider you host with. You can even fully instrument your on-premesis applications in minutes.

##This must cost the earth though, right?

In short, No it doesn't have to cost a penny. You can get started with a free account which should be plenty for a lot of smaller hobbyist sites.

But for businesses or your more popular sites you will want to look at the paid plans once you start capturing more data than the free plan provides. That threshold comes once you log 5 million data points over the month. Session data is free and unlimited, so these data points cover other types of info including (but not limited to):

* Events
* Page views
* Dependency calls (to databases, external services/APIs etc)
* Requests
* Performance counters

While the service is in preview, you can get the Standard and Premium plans at a discounted price of ┬ú14.97 and ┬ú60.78 per month, and the pay back can be hugely rewarding with the knowledge you'll unlock.

##How quick can I be up and running?

In minutes, seriously.

There are two paths to go down that depend on your situation and partly where your application runs.

Deploy Application Insights at **run time** to add instrumentation to an already running web app running on IIS, Azure Web Apps, or J2EE; with zero updates to your code.

Or if you don't mind making a few minor changes, setup Application Insights at **development time** to give you the ultimate control over web and desktop apps.

I went with development time changes when adding Application Insights to one of our larger multi-tenanted sites only last week and it was pretty straight forward. After adding a few NuGet packages and tweaking a config file we had almost realtime activity appearing via the Azure Portal.

I'm still learning my way around the power of it all. The basics come quickly and easily, but a lot of the power is tucked away in the analytics and proactive issue detection that comes as your data grows.

So now you know the basics, why not [get started for free](https://portal.azure.com/#gallery/Microsoft.AppInsights) and kick the wheels?