---
layout: post
title: An introduction to Azure Functions
date: '2016-10-11 17:00:00'
tags:
- it
- development
- net
- azure
---

If you already know about WebJobs, [Azure Functions](https://azure.microsoft.com/en-us/services/functions/) can be seen as an evolution, bringing with it quicker setup, easier management, and a lot more functionality. For those of you who haven't used WebJobs before, a [WebJob allows you to run background tasks in Azure](https://azure.microsoft.com/en-gb/documentation/articles/web-sites-create-web-jobs/) within the context of your App Service. There is no additional cost involved as your WebJobs sit within your web app, meaning you can take advantage of the same resources you dedicate to your web app already.

[Azure Functions](https://azure.microsoft.com/en-us/services/functions/) take this a step further and is positioned as a its own product within the Azure platform rather than a lesser-known feature of [App Services](https://azure.microsoft.com/en-gb/services/app-service/) web apps. Without delving in to the inner workings, Azure Functions are small bits of code (hence the functions name) that stand alone, operate and can be called independently of your other functions. Azure Functions are Microsoft's answer to AWS Lambda. 

You can think of an Azure Function almost as a Web API method. Input comes in (akin to a HTTP request in the Web API world), it matches the function (based on the URI), some code runs, and there is some output (a HTTP response when talking about Web API).

###So this is just Web API then?

Well no, Azure Functions is more high level than that. I'm sure Web API (or some component of it) is involved down in the lower levels somewhere, but you don't need to think about it, or anything else other than the code you want to write. Forget writing controllers, forget routing, forget a lot of things. Just jump straight in to solving your business problem and moving on to the next.

If you have ever used [IFTTT](https://ifttt.com/recipes) you're in the same ballpark with Azure Functions. You define your trigger (the "this" of If-this-then-that), your code runs and produces some output (the "that" of If-this-then-that). Microsoft provide a number of triggers out of the box:

- **BlobTrigger** - run your function when a blob is added to a container
- **EventHookTrigger** - run your function when a new event is received
- **Webhook** - run your function when a webhook request is received
- **GitHub Webhook** - run your function when a web hook is received from GitHub
- **HttpTrigger** - run your function when it receives a HTTP request
- **ManualTrigger** - run your function when you choose by clicking a "Run" button
- **QueueTrigger** - run your function when a message is added to an Azure Storage queue
- **ServiceBusQueueTrigger** - run your function when a message is added to a Service Bus queue
- **ServiceBusTopicTrigger** - run your function when a message is added to a Service Bus topic
- **TimerTrigger** - run your function on a custom schedule

With Azure Functions still in preview, I'm sure new triggers will appear by the time it reaches general availability, but even now the above triggers give you so much potential.

You may be wondering how you write your function. Well let me say that with this new Microsoft, they aren't forcing you to use C#. Yes C# is there and supported but so is NodeJS. There's even F# support in the works too for the functional crew amongst us.

![Editing a function](/content/images/2016/10/azure-functions-screenshot-1.png)

Writing your function is as easy as it could be. No IDE to mess around with, no SDK to download (although I'm certain you could do both if you wish); simply point your browser at the [Azure Portal](https://portal.azure.com) and create away. Make changes until you are happy and with one click of the Save button your code is compiled and ready to be triggered. No packaging, no uploading, no deployment - click and run.

On the other side of your function, you can output in a number of different ways again. Other than sending back a traditional HTTP response to the caller, you could...

- Create a blob in Azure Storage
- Add a record to an Azure Storage Table
- Add a message to an Azure Storage Queue
- Add a message to an Azure Event Hub
- Add a message to Azure Service Bus
- Add a document to Azure DocumentDB
- Add a record to an Azure Mobile Table
- Add a message to an Azure Notification Hub
- Send an e-mail via SendGrid
- Send an SMS via Twilio


The magic of Azure Functions means you don't need to concern yourself with how any of these services work. That's all done for you using bindings which makes it as easy as writing a little JSON and setting some variables in your function.

###How is this better than writing your own Web API or WebJob?

For starters, you don't need to think about the infrastructure or the mountains of boilerplate code you need to write to create an ASP.NET Web API site. And you don't need to think about packaging and deploying your WebJob and the WebJobs sharing resources with your web app.

With Azure Functions you can focus on what is important to you. Think of things in terms of events and action those events however you need to. Put the concepts of a web server, web app and frameworks to the back of your mind and dive in.

Some people call this going [*serverless*](https://en.wikipedia.org/wiki/Serverless_computing) but I personally dislike that term. No matter how much we are abstracted away from the underlying technology we all know there's a server involved. It is just no longer something we need to be involved in.

###What does it cost?

Unlike WebJobs where you are paying for a web app already, Azure Functions is priced on a combination of code execution time and the number of executions. The math is a little hard to get your head around to start with, but in simple terms, you choose how much memory your service needs and then pay a minuscule amount for the usage of that memory while you use it. If you don't call your function, you don't pay anything. Call it every second or require lots of memory and your costs will slowly increase.

However Microsoft are kind enough to give you a free monthly grant that lets you get started. That grant is rather generous and includes 1 million executions for free every month. With that you get 400,000 GB-s (Gigabit Seconds - how many gigabits of memory you need per second of operation) of execution time.

According to Microsoft's [pricing page](https://azure.microsoft.com/en-us/pricing/details/functions/) that means your function can execute for over 3 million seconds per month if using the minimal 128MB memory tier. Which is a huge amount of time when you consider a 30-day month runs at 2,592,000 seconds.

With that, there's no excuse not to find a reason to [give Azure Functions a try](https://azure.microsoft.com/en-us/services/functions/)!