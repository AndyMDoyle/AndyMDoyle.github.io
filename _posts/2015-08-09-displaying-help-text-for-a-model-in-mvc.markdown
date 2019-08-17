---
layout: post
title: Displaying help text for a model in MVC
date: '2015-08-09 10:03:00'
tags:
- development
- mvc
- asp-net
---

We've recently been working on a new MVC app consisting of a number of different models, each with their own set of CRUD pages. As things have grown in complexity thanks to [feature creep](https://en.wikipedia.org/wiki/Feature_creep), we have reached the point where we needed some quick and easy inline help alongside inputs in each view.

At first hard coding looked the way we'd go but that's messy right? Why not take a leaf out of MVC's book and use an [Attribute](https://msdn.microsoft.com/en-us/library/system.attribute(v=vs.110).aspx) to decorate the model and render this using a [HtmlHelper](https://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper(v=vs.118).aspx) extension method. It's a very simple process and a pretty clean way of doing it.

The starting point is the HelpTextAttribute that you can use to decorate your model. It is nothing more than the [DisplayAttribute](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayattribute(v=vs.110).aspx) with a new name:

```language-csharp,line-numbers,theme
namespace MySite
{
    /// <summary>
    /// Specifies the help message for a property
    /// </summary>
    public class HelpTextAttribute : DescriptionAttribute
    {
        /// <summary>
        /// Initializes a new instance of the HelpTextAttribute class with a help message.
        /// </summary>
        /// <param name="helpText">The help text</param>
        public HelpTextAttribute(string helpText) : base(helpText) { }
    }
}
```

Now you can decorate your model by adding ```[HelpText(string)]``` like so:

```language-csharp,line-numbers,theme
namespace MySite.Models
{
    public class Company
    {
        [Required]
        [Display(Name = "Company Name")]
        [HelpText("The legal entity name for this company")]
        public string CompanyName { get; set; }
    }
}
```

The hard(er) part comes in displaying this help text inside your view. A HtmlHelper extension method does the work here to accept a lambda expression to target a property of your model:

```language-csharp,line-numbers,theme
namespace MySite
{
    public static class HtmlHelperExtensions
    {
        public static string HelpTextFor<TModel, TValue>(this HtmlHelper<TModel> html, Expression<Func<TModel, TValue>> expression)
        {
            var memberExpression = expression.Body as MemberExpression;

            if (memberExpression == null)
            {
                throw new InvalidOperationException("Expression must be a valid member expression");
            }

            var attributes = memberExpression.Member.GetCustomAttributes(typeof(HelpTextAttribute), true);

            if (attributes.Length == 0)
            {
                return string.Empty;
            }

            var firstAttribute = attributes[0] as HelpTextAttribute;
            return html.Encode(firstAttribute?.Description ?? string.Empty);
        }
    } 
}
```

All that's left to do is display the help text where you need it in your view:

```language-csharp,line-numbers,theme
@Html.HelpTextFor(m => m.CompanyName)
```


Of course this could be extended to add localisation support without too much trouble. Instead of passing the help text to the HelpTextAttribute you could pass the key to a resource string, and have the HelpTextFor method from whatever resource manager you are using. But if all you need is simple help text in a single language, [YAGNI](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it).