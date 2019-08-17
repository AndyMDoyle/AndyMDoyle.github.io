---
layout: post
title: JavaScript reference directives and Visual Studio 2017
date: '2017-03-18 15:57:05'
tags:
- development
- visual-studio
- microsoft
---

[Visual Studio 2017](https://www.visualstudio.com/vs/) brings a lot of new functionality to the table; as you would expect from a major new release, but Microsoft appear to give with one hand and take away with the other.

Visual Studio 2017 introduces a new [JavaScript language service](https://docs.microsoft.com/en-us/visualstudio/ide/javascript-intellisense) that is used to power IntelliSense. The new language service is a big change and takes advantage of TypeScript under the hood. While all of this is great, it looks like there are some changes that could leave you scratching your head.

One key change I've discovered is that this new language service does not support reference directives, or at least it doesn't appear to work today. By that I mean using something like `/// <reference path="ScriptFile1.js" />` to instruct IntelliSense that you'd like it to scan an external JavaScript file to provide you with auto-complete for the external functions, types and fields from the referenced file.

We use reference directives quite extensively, throughout our projects and since ditching Visual Studio 2015 (about 2 hours after the Visual Studio 2017 hit release) I started wondering where my nice IntelliSense had gone. At first I put it down to reindexing the several dozen JavaScript files so didn't think too much of it. But days later and nothing has changed.

Whether this is a bug, or it has been left out of Visual Studio 2017 in favour of you using a module system or TypeScript definitions; I don't know. But I hope we can get it back in a future update.

For now, the great new Go To All feature helps quickly find and check the correct method signatures when I need to call an external method.