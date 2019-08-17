---
layout: post
title: 'Octopus Deploy: Where we are today'
date: '2015-12-28 19:07:00'
tags:
- it
- development
- octopus-deploy
---


A lot of our web apps are hosted across multiple nodes and each environment sits behind a multi-node load balancer that handles the distribution of incoming requests. For a seamless deployment we need to take a web server out of service with the load balancers, upgrade the node, spin the sites back up, test it's alive and kicking, and then add the node back to the load balancer.

Originally we were manually executing PowerShell scripts to control the load balancing and a mixture of scripts and manual browser tests to do the rest. For our largest project we would be looking at close to 40 minutes of work to roll a new release out between three environments (not without proper testing in-between though!). And on a busy day we could release anywhere between 2-6 updates to our primary web app. What a waste of time!

After installing Octopus Deploy, it took a few tries to hone this process within the web-based management dashboard. But it was well worth the 10-15 minutes. With our environments and custom scripts now setup properly we can now have a new release pushed out to our development environment right from Visual Studio - without needing to touch Octopus Deploy at all. No one needs to think about it, no one notices the sites go offline, no one spots any downtime and unless you were expecting it you wouldn't know anything had happened.

That's how DevOps should be.

Today we have over 10 projects managed by Octopus Deploy with several environments spread across on-prem servers and up in Microsoft Azure. It deploys our web apps, Windows Services, and even some internally-developed command-line tools used by Windows Task Scheduler around the company. 

Without Octopus Deploy we would be spending a great deal more of our time deploying new releases, meaning less time on the important part - developing new features and (occasional) bug fixes.

In a later post I will cover our plans to make the most of Octopus Deploy, and hopefully, how we streamline even further.