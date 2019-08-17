---
layout: post
title: Azure Web Apps - beware the phantom deployment slots
date: '2017-08-18 17:00:00'
tags:
- it
- azure
- powershell
---

As I've mentioned [in previous posts](/tag/octopus-deploy/), we use [Octopus Deploy](https://octopus.com) to handle our deployments on-prem and to Azure. Last week I was doing some maintenence and decided to update some old PowerShell scripts to use the new Azure Resource Manager cmdlets rather than the old Azure Service Management cmdlets.

The reason for this is that moving forward, all new functionality is exposed using AzureRM; and this is what the new [Azure Portal](http://portal.azure.com) is built upon. Coincidentally just days earlier we came across an issue running the old ```New-AzureWebsite``` cmdlet; and it took a while for Microsoft to recognise and fix the issue, so I wanted to move away from the old ways.

A lot of our Web Apps are deployed using a process along these lines:

1. Remove the deployment slot named "staging"
2. Create a new deployment slot named "staging"
3. Publish the files to this new slot
4. Hit the staging deployment slot to warm up the site
5. Swap the staging and production slots around
 

Quite simple, and it has worked for years.

After working through a couple of sites and updating the scripts, I reached a rather old web app that was created long before AzureRM was a thing. That shouldn't be a problem though as AzureRM can be used to manage Web Apps regardless of when they were created.

However the first deployment of this site following the change resulted in a dreaded red warning message informing me that the deployment had failed. The PowerShell output indicated rather vaguely that the "staging" deployment slot couldn't be found - so it couldn't be deleted.

After confirming the deployment slot was indeed there, by visiting https://mysite-staging.azurewebsites.net I started digging deeper.

The output from ```Get-AzureWebsite``` showed the staging slot - that made sense as the site was there running. But ```Get-AzureRmWebAppSlot``` didn't. And neither did the Azure Portal.

Being a staging slot it didn't have anything that wasn't about to be nuked, so I deleted the staging slot using ```Remove-AzureWebsite -Name mysite -Slot staging``` and recreated it using ```New-AzureWebsite -Name mysite -Slot staging```.

As if my magic, this new staging slot popped up in the Azure Portal and could also be found using the AzureRM cmdlets!

I don't yet know if this is a common issue, or if there was a problem with this one site, but it appears that Azure got a little confused somewhere and AzureRM wasn't aware of this old deployment slot.

So, if you find yourself unable to create or delete a staging slot using ```New-AzureWebAppSlot```, check that it doesn't exist through Azure Service Management first.