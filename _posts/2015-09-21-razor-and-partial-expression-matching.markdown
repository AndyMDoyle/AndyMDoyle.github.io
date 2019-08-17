---
layout: post
title: Razor and partial expression matching
date: '2015-09-21 07:00:00'
tags:
- development
- c
- quick-fix
---

[ASP.NET Razor](http://www.asp.net/web-pages/overview/getting-started/introducing-razor-syntax-(c)) is an amazing server-side markup language that allows developers to use their existing C#/VB language skills. If you're used ASP.NET Web Pages or MVC you've probably used Razor whether you know it or not. Razor is all of the stuff you decorate with an @ prefix, dotted throughout your HTML code as if it was part of the HTML specification.

You've probably written statements like this loads of times:

```language-aspnet,line-numbers,theme
<!-- A single statement -->
@{ var myValue = 2; }

<!-- An inline expression (mixed with HTML) -->
<div id="divResult">Your starting value is @myValue</div>

<!-- A multi-line statement block -->
@{
  var myValue = 2;
  var multiplier = 5;
  var result = myValue * multiplier;
}
Your result is @result
```

Those are quite basic examples and sometimes you have a more complex statement or you want to output an inline expression constructed from two or more variables or pieces of data.

I came across this exact scenario recently and was surprised to see that the Razor engine doesn't read-ahead too much. Instead it stops interpreting Razor syntax as soon as it encounters a space that isn't enclosed in a string.

So something like:

```language-aspnet,theme
@Model.LastUpdatedBy ?? "N/A"
```

results in

```language-markup,theme
Some User ?? "N/A"
```

Do you see what's gone wrong? The Razor engine outputs the result of @Model.LastUpdatedBy, but as the next character is a space, parsing of the syntax ends and the remainder of the line is treated as plain-old HTML.

The good news is there is a very simple, and rather obvious fix. To instruct the Razor engine to treat the whole line as a single statement you just need to wrap your code in parentheses.

```language-aspnet,theme
@(Model.LastUpdatedBy ?? "N/A")
```

then gives you the expected result of:

```language-markup,theme
Some User
```

If only all issues were this easy to resolve!