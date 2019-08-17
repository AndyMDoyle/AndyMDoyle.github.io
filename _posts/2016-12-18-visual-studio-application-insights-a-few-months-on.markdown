---
layout: post
title: Visual Studio Application Insights - a few months on
date: '2016-12-18 14:16:00'
tags:
- application-insights
- devops
- development
- it
---

Several months ago [I spent some time looking at Application Insights](/visual-studio-application-insights-an-overview/), which at the time was part of the Visual Studio family of tools and services. Well as we've seen before, it looks like Microsoft have had a rethink and have renamed Visual Studio Application Insights and have moved it back under the [Azure umbrella](https://azure.microsoft.com/en-gb/services/application-insights/). It is a subtle change, but the [Visual Studio product page](https://www.visualstudio.com/products/) lists it clearly as "Azure Application Insights" now.

Brand change aside, I've not been able to put Application Insights through its paces so I thought I would follow up with how things were going, and the issues that occurred on the way.

##What I liked
This is a tough starting point. Overall I am very impressed with what Application Insights offers and how it can help a DevOps team. It would be much easier to start by listing the niggles or issues first as that list is much shorter. But I don't want to kick off by listing the negatives.

###Instant visibility
At any time you can refer to the Azure Portal to check on the health of your app. There isn't a single healthy/unhealthy indicator you can look, but by customizing the dashboard you can bubble up the metrics that are important to you and your application. Don't care about 404 errors? Ditch it. Don't need to track the daily visitors you've had? Ditch it. Start by thinking about what is important to you. If you monitor logs or other instrumentation manually right now, you could make a few tweaks to present this information on your dashboard so that you can see new events at a glance.

###Alerting
The web application we started off with is scaled across 6 web servers, all tucked away behind a reverse proxy powered by IIS Application Request Routing.

![Live streams of data arriving in Application Insights](/content/images/2017/01/Screen-Shot-2017-01-08-at-14.44.04.png)

Application Insights knows this because it sees 6 streams of data coming from different servers, and can use this data to alert me to any problems. If one of the streams was to stop for a while it can raise an alert (via e-mail and in the dashboard) so I can see that one of the nodes is misbehaving.

But that's only the basics - the tip of the iceberg really. Application Insights has a lot of power and machine learning capabilities behind the scenes and not only does it let you know when your custom alerts are triggered, but it can learn about your app and flag up potential issues early on.

For example, we've had a couple of bad releases over the last few months for one reason or another, and Application Insights is smart enough to detect an increase in exceptions in your application. It does this by monitoring normal usage and establishing a baseline of how your app works. Then when something abnormal happens (such as a steady flow of internal server errors, or 404 errors), it fires off an alert and e-mails you. A couple of times Application Insights has beat our existing logging and monitoring methods and we've been able to start troubleshooting quicker than normal. As applications grow in size, complexity or scale to more and more servers, it is amazing to be told where issues are happening so quickly.

###Usage metrics & server-side events

We've used Google Analytics for years and while it is a great product itself, Application Insights brings some extra tricks to the table. Yes, Google Analytics can show you visitor numbers and what pages they are visiting; but Application Insights adds to this a lot of server-side data that just isn't available from a client-side tool.

So not only do we see what pages visitors are looking at, their browser details, geo-location, operating system, page visits; but we can drill down to a request and actually see how long it took to process, where the time was spent in processing that request, and go as far as seeing the server-side dependencies. Those dependencies could be database queries, calls to WCF Services, HTTP services, or requests to Azure services such as querying Table Storage or retrieving a blob. All of these add to the response time and are invaluable in troubleshooting slow page load times.

##What I didn't like

While I limited myself to picking my top 3 likes above (because if you want to know what other cool stuff Application Insights can do, [you can read about it yourself](https://azure.microsoft.com/en-gb/services/application-insights/), or even [try out the free tier](/visual-studio-application-insights-getting-your-moneys-worth-out-of-the-free-plan/)), I can honestly only come up with two negatives so far.

###Maxing out the free and standard tiers

I have Application Insights running in a reasonably large and visited web app, and within a week the data allowance of the free tier was behind us and we had to scale up to the standard tier. Less than weeks later and e-mails start coming in to say the 15m data point quota was almost being reached again.

I didn't want to cough up for the Premium tier, but luckily Application Insights gives you another option - data sampling. Instead of processing every event sent to Application Insights, you can throttle this back to consume a fraction of the live data. While it does not give you perfect insights, you do still get a good idea of how things are operating.

So far I have only had to scale back to 50% sampling and that's enough to stay within the quota based on a daily data point figure of between 500k and 900k. As traffic and usage increases though, I'm happy in knowing I can turn the dial to cut the sampling down to 33%, 25% or even lower.

###No quick way to filter out noise

Every site generates 404 errors. Browsers alone can cause a fair amount when they look for browser-specific files such as icons, or metadata. Take Safari for instance... I see regular requests for app icons at different sizes both in their normal and precomposed forms. Our app does not have all of the different combinations of these so it results in a bunch of 404 errors in Application Insights.

It would have been great if these could be filtered out in the dashboard with a click or two; but instead you need to filter these out in the application itself. I did this by writing a noise filter, inheriting from `ITelemetryProcessor`, and performing some basic logic checks in the `bool OkToSend(ITelemetry item)` method. It isn't a big job, but it does require access to the source code of the application and for some modifications to be made.

##Will Application Insights be staying?

At the moment I'm happy, and don't feel the need to look elsewhere. I think I'm getting all of the metrics I could ever need. And when it comes to the cost, I have a nice balance between data sampling and monetary spend.

However there are some changes on the cards and Microsoft have announced [some big changes to their pricing tiers](https://azure.microsoft.com/en-gb/pricing/details/application-insights/). I haven't run the numbers yet, but hope that the changes won't hit the wallet.

So stay tuned...