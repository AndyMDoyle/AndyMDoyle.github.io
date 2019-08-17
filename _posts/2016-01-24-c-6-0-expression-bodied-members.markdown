---
layout: post
title: C# 6.0 - Expression Bodied Members
date: '2016-01-24 20:13:45'
tags:
- development
- c
---

It seems like a long time since Visual Studio 2015 was launched and brought us the new language features of C# 6.0 - it was a whole year ago if you go by the 2015-nomenclature. None the less I'm still finding these new language improvements a bit of a novelty especially when you think about how our code would have looked before them.

I find I have already thrown out manual string concatenation and string.Format in a lot of my day-to-day activities and replaced it almost exclusively with [string interpolation](/c-6-0-string-interpolation/) that I covered a couple of months ago.

Another feature that has crept in and is already helping improve code readability is expression bodied members. If you haven't heard of expression bodied members, or simple expression bodies as some people call it, it is a way of writing the block of code normally found representing a function body as a simple lambda expression. Here's an example with a rather simple class:

```language-csharp,line-numbers,theme
public class Person
{

    public string FirstName { get; set; }
    public string LastName { get; set; }

    public string FullName
    { 
        get
        {
            return $"{FirstName} {LastName}";
        }
    }

    public override string ToString()
    {
        return $"First name: {FirstName}; Last name: {LastName}";
    }
}
```

With the power of expression bodied members this could be simplified to:

```language-csharp,line-numbers,theme
public class Person
{

    public string FirstName { get; set; }
    public string LastName { get; set; }

    public string FullName => $"{FirstName} {LastName}";

    public override string ToString() => $"First name: {FirstName}; Last name: {LastName}";
}
```

Notice how the FullName property and the overridden ToString() method has lost the curly braces, return keyword? After the normal property of method declaration the ```=>``` (aka the lambda arrow or fat arrow) indicates that expression to the right will be returned as the value.

While it hasn't saved a great deal of keypresses it does look a lot neater especially where the code was initially short and simple. Expression bodies can't replace multiple line code blocks so you won't be able to replace all of your current member declarations with expression bodied member declarations. So while a nice improvement it isn't a complete change or replacement of the traditional curly brace code blocks.

You may have also noticed in the above example that FullName is a getter-only property. Expression bodies lend themselves perfectly to this use-case. It isn't possible to use an expression body to replace a normal get/set property so don't waste your time trying!

If you want to try these out but don't have access to Visual Studio 2015, [I highly recommend LINQPad](/linqpad-the-ultimate-code-scratchpad/) as a great code playground. You'll want to grab version 5 as [LINQPad 5 fully supports the new language features in C# 6.0](/linqpad-5-get-it-now/).
