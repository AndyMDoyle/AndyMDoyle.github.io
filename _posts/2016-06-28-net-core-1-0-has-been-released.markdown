---
layout: post
title: ".NET Core 1.0 has been released"
date: '2016-06-28 09:46:00'
tags:
- development
- net
---

[![.NET Core - https://www.microsoft.com/net/core](/content/images/2016/06/Screen-Shot-2016-06-28-at-10-47-33-1.png)](https://www.microsoft.com/net/core)

[It's here](https://www.microsoft.com/net/core)! After many years of hard work by Microsoft, we have now moved in to a true cross-platform .NET world.

.NET Core is a brand new platform built from the ground up that allows developers to create web apps, services, and applications that run on Windows, Linux and Mac. Yes you read that right, you can truly write-once and run your code on the OS of your choice.

##What do I need to get started?

A box running Windows, Linux or OS X/MacOS is a useful starting point.

*A note on Linux... If you are running a rare distribution of Linux your mileage may vary, but if you are using one of the mainstream distributions (RHEL, Ubuntu, Debian, Fedora, CentOS, openSUSE) you should be good.*

###For development

For development you are going to need the .NET Core SDK. These are available as an installer for a few Operating Systems, otherwise you can get the .NET Core SDK binaries in an archive and extract them manually.

You will notice that the .NET Core SDK is labelled "Preview 2". The reason for this is that although .NET Core itself has been released, the tooling is a little behind and is still being baked. Although the tools are in preview, the .NET Core components are fully released and at version 1.0.

Next you will need a code editor or IDE. As we are talking cross-platform here, the obvious choice is [Visual Studio Code](https://www.visualstudio.com/products/code-vs). If you haven't already used Visual Studio Code, it's a relatively new code editor from Microsoft, which is ideal because it too is available on Windows, Linux and OS X.

After installing VS Code, the first thing I recommend you do is install the free [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp).

Windows users with the full Visual Studio 2015 IDE can grab [Visual Studio 2015 Update 3](http://go.microsoft.com/fwlink/?LinkId=691129) which brings you a bunch of .NET Core support and tooling.

From there, head over to the [Microsoft .NET Core documentation site](https://docs.microsoft.com/en-us/dotnet/articles/core/index) and take a look at the [tutorials](https://docs.microsoft.com/en-us/dotnet/articles/core/tutorials/index).

###For running apps with the .NET Core runtime

Download the .NET Core Installer, or .NET Core binaries.

These contain the runtime only and don't include any of the SDK or CLI tools required for development. This is what you would install on your production machines.

##Find out more

Here are the key blogs announcing this in more detail:

* [.NET Blog - Announcing .NET Core 1.0](https://blogs.msdn.microsoft.com/dotnet/2016/06/27/announcing-net-core-1-0/)
* [.NET Web Development and Tools Blog - Announcing ASP.NET Core 1.0](https://blogs.msdn.microsoft.com/webdev/2016/06/27/announcing-asp-net-core-1-0/)
* [The Visual Studio Blog - Visual Studio 2015 Update 3 and .NET Core 1.0 Available Now](https://blogs.msdn.microsoft.com/visualstudio/2016/06/27/visual-studio-2015-update-3-and-net-core-1-0-available-now/)
* [Scott Hanselman - .NET Core 1.0 is now released!](http://www.hanselman.com/blog/NETCore10IsNowReleased.aspx)