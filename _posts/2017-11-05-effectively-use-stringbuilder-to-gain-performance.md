---
title: "Effectively use StringBuilder to gain Performance"
date: 2017-11-05
categories: 
  - "dotnet"
  - "csharp"
tags: 
  - "net"
  - "c"
  - "csharp"
  - "dotnet"
  - "performance"
redirect_from:
  - "/effectively-use-stringbuilder-to-gain-performance/"
  - "/effectively-use-stringbuilder-to-gain-performance"
---

High performance of application is implicit requirement, no one states it, and however it’s there and supposed to be taken care of. Here is my first blog on StringBuilder that hopefully help you to sharpen your skills and become an [excellent C# developer](https://vaibhavgawali.net/excellent-csharp-dotnet-developer-skills/). (This is written after so many [observations from code reviews](https://vaibhavgawali.net/observations-from-code-reviews-and-why-they-are-important/)) and from my personal experiences.

Using StringBuilder is the most recommended way to concatenate large chunks of strings , mostly this happens in loop. It is the best approach to take, and despite this I have seen many developers not to follow this practice.

I have also seen developer’s instantiating StringBuilder in an inefficient ways too. You should effectively use StringBuilder to gain performance, and below are the guidelines for some efficient ways to use StringBuilder & get some performance.

- Always try to instantiate StringBuilder with some default value or capacity
- Use in large loops or at places where most of the concatenations are happening
- Use the same instance of StringBuilder in all methods that construct a single string

Example code:

```csharp
static void Main(string[] args)
{
    int guessLength = 30;
    StringBuilder sb = new StringBuilder(100 * guessLength); //Give capacity or value as far as possible
    for (int loop = 0; loop < 100; loop++)
    {
        sb.Append(loop).Append(":").AppendLine();
    }
    ConstructMessage(sb);
    ConstructAdditionalMessage(sb);
    Console.WriteLine(sb);
}

static void ConstructMessage(StringBuilder sb)
{
    for (int loop = 0; loop < 5; loop++)
    {
        sb.AppendFormat("{0}:{1}", loop.ToString(CultureInfo.InvariantCulture), Environment.NewLine);
    }

}
static void ConstructAdditionalMessage(StringBuilder sb)
{
    sb.AppendLine();
    for (int loop = 0; loop < 5; loop++)
    {
        sb.AppendFormat("{0}:{1}", loop.ToString(CultureInfo.InvariantCulture), Environment.NewLine);
    }
}
```

 

Can you guess why I have used “loop.ToString(CultureInfo.InvariantCulture)” in the above example code?

Related readings:

[https://www.dotnetperls.com/stringbuilder-performance](https://www.dotnetperls.com/stringbuilder-performance)

[http://stackoverflow.com/questions/1612797/string-concatenation-vs-string-builder-performance](http://stackoverflow.com/questions/1612797/string-concatenation-vs-string-builder-performance)

![Effectively use StringBuilder](/assets/images/effectively-use-stringbuilder-to-gain-performance/Effectively-use-StringBuilder.png)
