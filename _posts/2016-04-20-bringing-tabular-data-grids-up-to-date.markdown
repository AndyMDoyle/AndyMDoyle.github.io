---
layout: post
title: Bringing our data grids up to date
date: '2016-04-20 06:53:54'
tags:
- development
- asp-net
- syncfusion
---

If you develop ASP.NET web apps, how many times have you been working on a new page and simply thrown a GridView control on there or rendered a plain old `<table>` in your MVC view?

I know I probably do it at least a few times a week. But have you stopped to think for a moment about what else is out there that, a) could be easier to integrate, and b) would empower your users or visitors?

That's exactly what we did on a recent project and the outcome has been very positive by both developers and users. From the start we already knew this internal sales tool would lead to any number of future requests for custom reports or requests for assistance when someone forgets how to do something in Excel. So we had the idea of throwing out plain old tables and implementing a rich and powerful third-party component to give the power to the user, right there in the browser.

If you spent 5 minutes [looking around right now](https://www.google.co.uk/#q=jquery+data+grid+plugin) you'll be surprised at just how many options there are in the form of jQuery plugins, let alone what you'll find for other popular Javascript frameworks. There are so many choices and sadly, as is quite common, many of them are [abandonware](https://en.wikipedia.org/wiki/Abandonware).

So we started with what appeared to be the most popular free options and began testing them out. Some fell early on and we didn't bother going past playing with their online demos, and others we felt were techncially suitable but lacked the community to drive it forward or to support us if we committed ourselves to that particular product.

When we had a short list down we then had a look at the big commercial options that generally come in the form of developer toolkits - a bundle full of dozens of different components that should provide you with all of the UI elements you may want for your web apps.

The one that stood out for us was [Syncfusion](http://www.syncfusion.com), who provides components for ASP.NET WebForms, ASP.NET MVC, and Javascript. Oh and LightSwitch and Silverlight too but are many people still using those? They also have products for mobile and desktop development, so they could be your ideal one-stop-shop.

After building out some test pages for each candidate it was clear the commercial options were the best choice despite some varying price tags, and following a lot of testing dialog with Syncfusion we were given the opportunity to try their Essential Studio product (including support) for 3 months with no commitment to buy. A company who offers that on top of a standard 30 day trial must be confident that they'll stand up well against their competitors. So we jumped at the opportunity.

Here's an example of what their javascript-based grid can do:

![Syncfusion ejGrid example](https://www.syncfusion.com/products/aspnetmvc/images/ejgrid/ejg_sorting_grouping.png)

Okay so it may not win awards for the prettiest grid but there are numerous themes to choose from, a Bootstrap theme to make it look at home if you use Bootstrap, and Syncfusion even offer a new theme studio where you can build your own theme with a few clicks. Or if you're like us, you can hack around and build your own CSS stylesheet by hand.

Looks aside, functionality isn't shortcoming. Pitched against a mid-level Excel user I don't think this grid would fall short and we've found that since implementing it, we've had zero requests for an option to export the data to Excel for further manipulation. That wouldn't be hard though as exporting to Excel, Word and PDF is an out of the box feature - we just haven't flicked that switch yet.