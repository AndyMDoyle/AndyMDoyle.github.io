---
layout: post
title: A problem with tight coupling
date: '2016-05-30 18:56:00'
tags:
- development
---

How many times have you looked back at old code and felt ashamed? Not because it was terrible code or didn't work, but because it doesn't adhere to the standards, processes or best-practices we know and follow today.

That happened to me this week when I discovered a classic case of [tight coupling](https://en.wikipedia.org/wiki/Coupling_(computer_programming)) between two objects that should have been kept at arms length, or at least implemented in a less rigid way. Tightly coupled code normally results in a ripple effect when one element changes, as even the smallest change can break the other components. It's like a domino effect - you change one thing and everything else in close proximity starts to fall over.

Earlier this week I started planning for a database migration, where we aim to take move some key business database over to a new 2-node active/passive SQL Server cluster. Part of the planning was cataloging the databases, discovering which clients are using them, and what else may touch these databases as they stand today.

After scouring the SQL Server logs I found all of the expected clients - web servers, application servers and so on. But what I didn't expect to see were occasional connections from a number of Windows Servers running Remote Desktop Services. The only thing these run is our ERP package from SAP and the SAP client shouldn't know of our other databases at all.

It is perfectly normal for this client application to connect to our SQL Server though as it relies on a number of SAP databases, but these connections were to one of our own databases used by one of our web apps. Odd indeed.

Tracking things down thanks to the application name in the SQL Server connection string, it turned out to be an add-on we developed in-house for our ERP package. This was developed getting on for 10 years ago and "just works" so there hasn't been the need to touch or update it since so it has slipped to the back of our minds.

Pulling down the source code from our repository I was happy to find it opened perfectly in Visual Studio 2015 and even built first time. Quite a surprise since it had been built back in the Visual Studio 2008/2010 days! However the happiness soon passed when I saw the reason for the database connections. One function of this add-on is to perform some additional business logic when an incoming payment was logged via the SAP client, and part of this workflow involved writing details of the transaction to a database directly.

That's not too uncommon I'm sure, but the biggest concern was that it used a hard-coded connection string, naming a specific hostname and database name right in the CS file. Had we moved these databases without checking the logs first, this client would have thrown a fit every time someone logged a new payment and it could have taken a while to track down.

***So what's the problem with that?***

Nothing at first. When you write code like this and hard code a connection string you'll get it built, tested and deployed without problem just like we did. But roll forward some time and a number of events could shatter this, namely:

- You rename your SQL Server
- You retire/replace your SQL Server
- You rename the database (less likely but still possible)
- You move the database to another instance or server
- You change the database or table schema

The moment any of those things happen, without proper planning you will be fire-fighting and taking calls from users when they start receiving errors.

***How should it be done?***

There are a few small improvements that could be made to address the above scenarios, and a bigger one that we have ultimately chosen to follow, of which I will follow up with another blog post soon.

The quick fixes here would firstly remove the dependency on a specific SQL Server. At the moment the Windows hostname is hard coded right in to the connection string so if that server goes offline or changes for whatever reason, the client can't connect.

SQL Server has a little-known feature called Hostname Aliases. You can quite quickly [configure an instance of SQL Server with an alternate name (or alias)](https://msdn.microsoft.com/en-GB/library/ms190445.aspx) that can be ported to another instance or server when required. Think of this as a CNAME record in DNS so you don't have to refer to the static Windows hostname.

We could create a new alias for ```my-addon.domain.tld``` with SQL Server, create a matching CNAME record in DNS to point ```my-addon.domain.tld``` to ```current-sql-server.domain.tld```, and use ```my-addon.domain.tld``` in the connection string.

That's one part of it, but still having a hard-coded connection string is bad. It will require the application to be recompiled, versioned, packaged and deployed to all clients when a change needs to be made.

A cleaner option would be to store the connection string in an application configuration file, or (less desirably) the Windows Registry. With this you can alter the configuration settings independently of your code.

***But what about database or table schema changes?***

Now we have a cleaner way of connecting to the database, it doesn't help things if someone makes changes to the database schema or in the case of this add-on, the schema of the table it writes to. The client itself here has to know the structure of the table, and how to write to it. And this doesn't cut it for me today, and needs to change.

In C# we have interfaces that can act as a contract in a client/server setup, defining the methods/actions/structure available to a client to use. We don't have this in the SQL world so we need another intermediary who can act as a gateway for dozens of instances of this add-on.

If we were developing an application to run on home computers and it needed to access data from an on-premises database we wouldn't allow our SQL Server to be published directly to the internet and allow direct SQL connections. We'd have to be mad!

In this scenario we would have a web service that the "client" communicated with to retrieve data and perform actions. So why not do the same thing here?

A simple web service of some sort would allow all database-interaction to be performed centrally by the service, leaving the client to simply pass data to the service. The client no longer needs to know about the SQL Server, the database, or the table. And if we needed to change the business logic later, we only need to update this single web service rather than updating code running on dozens of machines.

So that's what we did, and in the next post I will introduce [Nancy](http://nancyfx.org) and how we used Nancy to build a very small and lightweight web-based API service.