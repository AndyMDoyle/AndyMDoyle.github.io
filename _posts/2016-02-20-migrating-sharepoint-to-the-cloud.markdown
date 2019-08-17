---
layout: post
title: Migrating SharePoint to the cloud
date: '2016-02-20 14:05:15'
tags:
- it
- sharepoint
- office-365
---

For well over 10 years we've been running SharePoint on premises. It all started with [SharePoint Team Services back in 2002-2003](https://en.wikipedia.org/wiki/SharePoint#Versions) and from there we've been through all major versions, and today our small on-prem setup consists of several sites collections, numerous sub-sites and some customisation to meet our organisation requirements.

With SharePoint Server 2016 on the horizon (and [now in RC](https://blogs.office.com/2016/01/20/sharepoint-server-2016-and-project-server-2016-release-candidate-available/)) I felt it was about time to take action and head off the (not-so-much) fun a SharePoint upgrade can bring.

In early 2015 we jumped on the Office 365 train initially as a cost saving effort when it came to renewing our Open Value Subscription that we licensed the Office Suite through. Doing so allowed us to license Office for our users at a lower cost, as well as including a few other Office 365 services to sweeten the deal.

One of these was extra services we receive as part of our Office 365 subscription is [SharePoint Online](https://products.office.com/en-gb/sharepoint/sharepoint-online-collaboration-software). If you are looking at SharePoint Online I think the first sentence on that page really sells it to the IT Pro.

>SharePoint Online delivers the powerful features of SharePoint without the associated overhead of managing the infrastructure on your own.

It pretty much sums up the whole cloud movement everyone talks about, and being the old person with SharePoint experience at our company I felt it was a smart move to, erm, move to SharePoint Online. After all we're already paying for it as part of our Office 365 subscription, so why not let Microsoft worry maintaining our SharePoint setup, handle the patching and hopefully soon, the upgrade to SharePoint Server 2016.

Anyway with top-level approval we kicked off by investigating the numerous options available in migrating to SharePoint Online. I won't go in to the detail of it all but there are some manual and long-winded options, and some very smart options depending on scale, amount of data, complexity of your setup and budget available.

After weeks of testing offerings from [Sharegate](http://en.share-gate.com), [Thinkscape](http://www.thinkscape.com), [AvePoint](http://www.avepoint.com/products/sharepoint-infrastructure-management/sharepoint-migration/), [Dell](http://software.dell.com/products/migration-suite-for-sharepoint/), and [Metalogix](http://www.metalogix.com), we settled on one of the newer Metalogix family members - [Essentials for Office 365](https://mv.metalogix.com/landing-page/essentials-office-365). Originally developed by MetaVis and [acquired by Metalogix in 2015](http://www.metalogix.com/News-Detail/2015/04/01/metalogix-acquires-metavis-technologies-to-accelerate-cloud-platform-growth), Essentials for Office 365 ticked all of the boxes when it came to migration but brings much more to the table.

Some of the tools we tried are just that - migration tools - and once that job is done there is very little chance you would touch them again. But Essentials for Office 365 includes management, security and reporting functionality that will make your life easier well after the migration is over.

It is still early days but we've already migrated a few site collections and a fair about of data but so far it has happened without a single problem.

Once I've had more time to try out all of the other features of Essentials for Office 365 I may follow this up with another post. But for now, if you are involved in a SharePoint migration or your company is moving to Office 365, I recommend you  [download a trial of Essentials for Office 365](https://mv.metalogix.com/landing-page/essentials-office-365) and give it a go.