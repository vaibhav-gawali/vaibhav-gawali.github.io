---
title: "Avoid Boxing and Unboxing to improve performance"
date: 2017-11-05
categories: 
  - "dotnet"
  - "csharp"
tags: 
  - "net"
  - "c"
  - "csharp"
  - "performance"
---

While writing code we generally don’t pay much attention to [boxing & unboxing](https://msdn.microsoft.com/en-us/library/yz2be5wk.aspx). It does matter in performance. And a [highly skilled and experienced C# / .NET developer](https://vaibhavgawali.net/excellent-csharp-dotnet-developer-skills/) must pay attention to everything that can improve performance.

[Here is an excerpt from MSDN article](https://msdn.microsoft.com/en-us/library/yz2be5wk.aspx):

> In relation to simple assignments, boxing and unboxing are computationally expensive processes. When a value type is boxed, a new object must be allocated and constructed. To a lesser degree, the cast required for unboxing is also expensive computationally.

[Side effects of boxing and unboxing](https://www.codingblocks.net/programming/boxing-and-unboxing-7-deadly-sins/):

1. Boxed value type objects take up more memory
2. Boxed value type objects require an additional read
3. Short-lived value type objects eat up Gen 0 heap & this forces frequent garbage collections
4. Boxing and unboxing operations consume CPU & time
5. Casting is required & it can be costly

How to prevent boxing & unboxing:

1. [Use ToString method of numeric data types such as int, double, float etc](http://stackoverflow.com/questions/6423452/boxing-and-unboxing-in-int-and-string).
2. Use for loop to enumerate on value type arrays or lists (do not use foreach loop or LINQ queries)
3. Use for loop to enumerate on characters of string (do not use foreach loop or LINQ queries)
4. [If you define your own value type then override implementation of basic object methods](http://stackoverflow.com/questions/24277239/calling-tostring-to-prevent-boxing).
5. [Don’t assign value type instance to object unless unavoidable](https://msdn.microsoft.com/en-us/library/yz2be5wk.aspx)
6. [Use generic List<>, Dictionary<> (et al) instead of ArrList & HashTable](https://msdn.microsoft.com/en-us/library/ms173196.aspx).
7. [Use Nullable<> value types (examples int?, float? etc)](http://stackoverflow.com/questions/4904514/is-there-a-performance-degradation-when-we-always-use-nullable-value-types-inste)
8. [When using string.Format (SrtingBuilder.AppendFormat) or similar API's that use 'params object\[\]' pass on value type objects by calling 'ToString()' method](http://stackoverflow.com/questions/8477322/boxing-and-unboxing-in-string-format-is-the-following-rationalized)

## Avoid Boxing and Unboxing to improve performance

Pay attention for below mentioned things & do some code refactoring

1. Implicit boxing (Example: object num = 1; )
2. Use of foreach on value types
3. LINQ queries on value type collections
4. Casting to value types

Here is my another post about [Effectively use StringBuilder to improve performance while concatenating strings](https://vaibhavgawali.net/effectively-use-stringbuilder-to-gain-performance/) which is related to similar performance topic.

![Boxing and Unboxing of value types](/assets/images/avoid-boxing-unboxing-improve-performance/BoxingUnboxing.png)
