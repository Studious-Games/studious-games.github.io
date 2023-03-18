---
layout: post
title: Unity Naming Conventions
date: 2022-04-25 22:55
category: [unity]
tags: [unity,programming]
---

Naming conventions or Coding Guidelines, is a way that helps not only a lone developer to organize the code better, but it also helps teams debug your code with ease as well as making the code consistent. It is a sensitive topic amongst a lot of developers, especially those who are adamant that they don't need to change. Which is fine, they have adopted what works for them.

But what about the rest of us getting started, or about to join a team in a new job.


## Why is that important?

- Consistent code Quality
- Coding Standards
- Naming Conventions



### Consistent Quality
When a developer or team is all using consistent guidelines, this makes it easier for everyone who is reading the code to understand and assimilate, what the intent of the code is doing. Even for the original author, this means the code is easily maintainable, as it is possible for a developer to not recall what a particular was written in a certain way, long after it is written. Conventions make this easier.


### Coding Standards
Designing standards, will help produce high quality code, that has been adopted by the organization or by following the guidelines for the language. With Unity and C#, Unity has recommended that developers adopt the conventions outlined by Microsoft.


### Naming Conventions
When following a naming convention, this reduces the time it takes to identify what the code is doing, what scope variables live and how methods are named.

Languages have what is called scopes for the variables, this means that a global variable can be used everywhere, and locally scoped variables can only be used inside the code block they are to be used. Each language tends to have a way to identify these scopes, where C# doesn't force you to prefix the variable with the scope it is intended for.

This is what can cause issues.

For example, generally in C# if you wish to use something that is defined globally for example, can be prefixed with the `this` keyword. As `this` denotes the current class, one can then use fields from that scope, however, it is not required as the language is smart enough to know where it lives. The problem is with us, unless we see where it lives, we can not assume what scope it actually is.

A common issue can then arise in some examples when you have code that looks like the following example.

```csharp
    private int width;
    private int height;

    public Setup(int width, int height)
    {
        width = width;
        height = height;
    }
```

As a developer, the `Method` has PascalCase and while the code does not have a summary to help document the code, if it did then we would be naming the parameters to identify what the intend of the inputs for the method are.

And as this is then used for a width and height for the class, it is kept to a minimum to help later on when it is used. It could be argued that it could be refactored to the following example.

```csharp
    private int imageWidth;
    private int imageHeight;

    public Setup(int width, int height)
    {
        width = width;
        height = height;
    }
```

However this then could cause over use of naming a variable and while we don't know what this class actually is here, if we then look at the class code in full we can see.

```csharp
public class Image
{
    private int imageWidth;
    private int imageHeight;

    public Setup(int width, int height)
    {
        width = width;
        height = height;
    }
}
```

I think you can see where I am going with this, we already know that the class is called Image, and that the fields are going to be based on a Width and Height. And we then look at the intent here, and as we already know the class is called Image, then the Width and Height, already shows intent. Naming it imageWidth would make it pointless.

This then leaves us with `private`, `public` as well as `protected` fields and properties, and usually this is where things get really get controversial.

I'll start with `public`, because this also applies to Methods regardless of their protection level. Public fields, and variables and all methods are supposed to be Pascal Case, the following example shows what this looks like.

```csharp
public class Image
{
    public int Width;
    public int Height;
}
```

The intent here is to let the developer see that the field here is public, no matter where the field is used in the `this` class or used in any other classes.

Now lets take a look at our first example, and refactor that to what Microsoft suggests we use.

```csharp
    #region private fields
    private int _width;
    private int _height;
    #endregion

    public Setup(int width, int height)
    {
        _width = width;
        _height = height;
    }
```

Now, to illustrate the intent here, I have placed the private fields into a region. As regions can be collapsed, you would then need to uncollapse the regions to know for sure, if there was no conventions used.

And this lies the problem, as a developer our work is hard enough trying to find and debug code as it is, without making the job ny harder than it is. If a naming convention or guideline, means that you are looking at one line of code. You are not moving your eyes away from that line, to see what scope that variable is. Yes, IDE's or decent ones, will color code these for you as well, but not all do and everyone has their code editor or IDE of choice.

The following example gives a quick over view to what I have already mentioned, as well as the other scopes that I haven't mentioned yet.

```csharp
// Classes - always PascalCase
public class ClassName : ISomeInterface // interfaces start with an "I"
{
    // Fields
    private int _privateField; // private fields camelCase with leading underscore
    protected bool _protectedField; // protected fields camelCase with leading underscore
    public string PublicField; // public is PascalCase. Prefer properties over public fields

    public const float PI = 3.14159f; // const is always SCREAMING_CAPS
    private const string MY_GREETING = "Hello";

    // Properties - always PascalCase
    public int RegularProperty { get => _privateField; protected set => _privateField = value; }
    public string AutoProperty { get; set; } // automatically creates its own backing field
    public bool GetOnlyProperty => _protectedField; // expression bodies to reduce number of lines

    // Methods - always PascalCase. Prefer being explicit with access modifiers like "private"
    private void PrivateMethod(int someParameter) // parameters always camelCase, no underscore
    {
        if (someParameter < _privateField) return; // use guard clauses to reduce indentations
        var someLocalVariable = 100; // local variables always camelCase, no underscore
    }
}
```

For Microsoft's Coding Guidelines :
<a href="https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions">Microsoft Coding Conventions</a>

