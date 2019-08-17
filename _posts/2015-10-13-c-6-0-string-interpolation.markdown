---
layout: post
title: C# 6.0 - String interpolation
date: '2015-10-13 07:27:26'
tags:
- development
- c
---

Hopefully you've had the time to play around with Visual Studio 2015 by now, and have got your hands dirty with the [new language features in C# 6.0](https://www.google.co.uk/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0CCIQFjAAahUKEwjOmKCD4ODHAhUFcNsKHbXCCco&url=https%3A%2F%2Fmsdn.microsoft.com%2Fen-us%2Fmagazine%2Fdn802602.aspx&usg=AFQjCNGtl2PUAhHtkWGNhkeQOwrVG6kdhg&sig2=BHJlkdugk08sZYZT7QBtng). While there are a few, a stand-out addition is the new string interpolation.

String interpolation is used to construct strings using a template-like syntax. If you've used [Handlebars](http://handlebarsjs.com) before, you'll see some similarities to how Handlebars binds values in your HTML templates.

Until now, the majority of us would have used [string concatenation](https://msdn.microsoft.com/en-us/library/ms228504.aspx) or [String.Format](https://msdn.microsoft.com/en-us/library/system.string.format(v=vs.110).aspx) to build your strings, mixing string literals and variables to construct the desired output.

Both methods had their drawbacks, the most common being the difficult to read code littered with + symbols, or {0/1/2/3/4/5/6...} placeholders. Neither really lent itself to improving code readability. Enter string interpolation which is a very welcome improvement.

Instead of inserting the {0} placeholder in a string literal and passing in the same number of parameters to String.Format, you can now reference the variable (or conditional expression) straight in your string.

##So how does it compare?

Here's a simple example containing all three options:

```language-csharp,line-numbers,theme
//Let's declare some variables
var firstName = "Bob";
var age = 25;

//String concatenation
Console.WriteLine("Hello " + firstName + ".\nYou are " + age + " year" + (age == 1 ? "" : "s") + " old.");


//String.Format
Console.WriteLine(string.Format("Hello {0}.\nYou are {1} year{2} old.", firstName, age, (age == 1 ? "" : "s")));

//New string interpolation
Console.WriteLine($"Hello {firstName}.\nYou are {age} year{(age == 1 ? "" : "s")} old.");
```

All three versions produce identical output, but notice how cleaner the final line is compared to the other using string concatenation or String.Format. The big difference is that you prefix your string with a $ symbol.

You'll not only see that firstName and age are used to construct the final string, but yo can also include a conditional expression by placing the expression inside the braces wrapped in parentheses.

##But can I still format values?

Yes you can and it's not as difficult as you'd think:

```language-csharp,line-numbers,theme
//String interpolation with formatting
Console.WriteLine($"Hello {firstName, 10}.\nYou are {age:D3} year{(age == 1 ? "" : "s")} old.");
```

The output of this is:

```
Hello        Bob.
You are 025 years old.
```

##How do I try this out?

You'll need an environment that supports version 6.0 of C# for starters. [Visual Studio 2015](https://www.visualstudio.com/vs-2015-product-editions) is the prime candidate and is available in both paid and free editions. But if you are looking for something a little lighter on disk usage, and a whole lot easier to jump in to, go and [download a free copy of LINQPad 5](http://www.linqpad.net).

I hope you see the benefits of this great new feature. It's a welcome addition to the language.

*Oh and if you prefer VB to C#, you aren't left out as string interpolation is also included in Visual Basic 14.*