---
layout: post
title: C# 6.0 - Null-conditional Operators
date: '2015-11-11 17:36:21'
tags:
- development
- c
---

Last month I introduced you to [the new string interpolation features of C# 6.0](/c-6-0-string-interpolation/), so in keeping with that theme I wanted to show you another of my favourite new features of C# 6.0 - Null-conditional Operators.

[Null-conditional Operators](https://msdn.microsoft.com/en-us/library/dn986595.aspx) are, according to the MSDN documentation, a way to check for null values before accessing a member or performing an operation on an index. Simplified it means you don't have to litter your code with if-null checks before accessing a property of an object.

##Member access

You know the code, it always goes something like this:

```language-csharp
public decimal CalculateItemPrice(ShoppingCartItem item)
{
    if (item == null)
    {
        return 0M;
    }

    if (item.Pricing == null)
    {
        return 0M;
    }

    return item.Pricing.Price * item.Quantity;
}
```

We've all written something like that and if you look at whatever project you are currently working on you will probably find dozens of those null checks scattered throughout your code-base.

Now let's see how this could look if we use Null-conditional Operators:

```language-csharp
public decimal CalculateItemPrice(ShoppingCartItem item)
{
    var price = item?.Pricing?.Price ?? 0;
    var quantity = item?.Quantity ?? 0;
    return price * quantity;
}
```

Cleaner right?

When accessing ```item?.Pricing?.Price```, if ```item``` is null a null value is returned from the expression and the rest of the chain isn't executed.

Assuming ```item``` is not null, it then checks the ```Pricing``` property. If it is null, a null value is returned and execution of the chain stops.

Finally if neither ```item``` or ```Pricing``` are null, then ```Price``` is returned. If at any point in this chain is null returned, the good old null-coalescing operator ensures that ```price``` is set to zero.

The same applies when obtaining the quantity. If ```item``` is null, ```quantity``` defaults to zero. 

##Index access

When accessing the index of a collection (array/list etc) the following code will check that ```articles[0]``` isn't null first. This is the index access part. Following on we are then using member access to check if ```CreatedOn``` is null. And to finish it off, if either are null we return ```DateTime.MinValue```.

```language-csharp
public DateTime GetDateOfFirstArticle(Article[] articles)
{
    return articles?[0]?.CreatedOn ?? DateTime.MinValue;
}
```

##Delegate invocation

This is something you're probably less likely to do on a day-to-day basis, but the Null-conditional Operator can also simplify invoking delegates. Consider this regular piece of code:

```language-csharp
var eventHandler = this.ValueChanged;
if (eventHandler != null)
{
    eventHandler(this, new EventArgs());
}
```

This can now be simplified like so:

```language-csharp
this.ValueChanged?.Invoke(this, new EventArgs());
```

I'm not sure how it could be cleaner or simpler but I'm sure the [.NET Team](https://twitter.com/dotnet) will have a go in a future version of C#.

I hope this quick run-through proves useful to you and helps you write shorter, cleaner code.