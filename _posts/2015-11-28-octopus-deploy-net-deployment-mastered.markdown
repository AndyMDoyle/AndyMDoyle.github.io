---
layout: post
title: Octopus Deploy - .NET deployment mastered
date: '2015-11-28 20:08:20'
tags:
- development
- it
- tools
- octopus-deploy
---

If there's one standout tool I've discovered this year it has to be [Octopus Deploy](https://octopus.com). I can't stress enough the hours this one product now saves us in our development cycle.

Seriously - back in the 'old' days (of a few months ago) we were manually pushing out several new releases per day across our dev, test and production environments; with each environment consisting of at least two nodes at any time. Sounds crazy when I think back about how things used to be.

On the road to where we are now, I toyed with a few different options to make life easier. I started by switching deployment of a couple of smaller projects to IIS Web Deploy and while it was a step in the right direction, it wasn't enough. [CruiseControl.NET](http://www.cruisecontrolnet.org), [Automatic](http://automic.com/products/automic-release-automation) and [a number of other tools](https://www.google.co.uk/search?q=.net automated deployment tools) looked good and we tried a few out but none stuck like [Octopus Deploy](https://octopus.com).

Octopus Deploy ([@OctopusDeploy](https://twitter.com/octopusdeploy)), for those who don't know, is a deployment automation tool specifically for .NET developers. It can integrate in to your development cycle in a number of ways and can be picked up quite quickly. That doesn't mean it is a simple product at all. While on the surface you can do a lot of common tasks with a few clicks of the mouse, its power really surfaces when you start utilising its PowerShell scripting abilities to tackle the more complex deployment scenarios.

Maybe I'll cover a little more on our specific uses in a later blog post, but for now I wanted to make sure Octopus Deploy was on your radar.

###What's this going to cost me?

In my opinion Octopus Deploy is worth every penny when it comes to the licensing costs. But you don't have to take my word for it. [Try it out yourself by grabbing a 45-day trial](https://octopus.com/downloads), after which the trial converts in to a ***FREE* Community Edition** that allows you to deploy up to 5 projects to up to 10 target machines.

We ran with the Community Edition for a couple of months but quickly [upgraded to a paid version](https://octopus.com/purchase) when we wanted to add some more projects.

And we haven't looked back since.

###Thoughts?

If you have already come across Octopus Deploy what did you think of it? And is it still part of your toolkit?
