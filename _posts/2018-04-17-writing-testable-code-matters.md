---
title: "Writing testable code matters"
date: 2018-04-17
categories: 
  - "dotnet"
  - "testing"
tags: 
  - "net"
  - "c"
  - "dotnet"
  - "testing"
  - "unittesting"
redirect_from:
  - "/writing-testable-code-matters/"
  - "/writing-testable-code-matters"
---

Do you tell your client “I cannot write testable code; writing testable code is not in my genes. My code is crap and it can only be tested with hard manual efforts; my code sucks and I am not a professional”. Do you think customers will come to you for the services you offer?

How about exact opposite stand – “[I am professional developer](https://vaibhavgawali.net/excellent-csharp-dotnet-developer-skills/), my code is 100% testable with full automation in place. And I am top 5% of the developers who can write testable code”.

I think you know the answer, customers will come to you, only when they know that you are good at developing top-notch software, not the other way around.

Most of the time, because of various reasons, it is very difficult to come up with a good unit test plan that can [cover every possible combination of inputs and external conditions](https://vaibhavgawali.net/are-you-doing-effective-testing/), and still meet the software release deadlines. And hence writing testable code is one of the challenges we face during software development life cycle.

In this post I am trying to address important aspects of “testable code” that will help you to become a professional C# .NET developer.  Be a pro my friend, not an a??hole, who can’t write testable code.

# Why should you care for writing testable code?

Number one reason is – “to maintain quality of the software”.

Subsequent reasons are – “to maintain quality of the software”.

What on earth tells you that there could be other reasons too?

Or perhaps you want to become a lazy nerd who just want to **“test the code for each code check-in, in an automated manner”.** Dam, you are my type ;).

# Where testable code will help?

To speedily execute unit test cases (MSTest, NUnit, xUnit etc.) in an effortless manner (i.e. without manual intervention) that gets triggered automatically for every code check-in.

To automate integration testing.

To automate UI testing.

We are taking all the pain just to find bugs as early as possible. (In good old earlier days, management used to fear instantly, whenever developers try to change even single line of code. This scenario is now changing with automation in place).

When a unit test case is added in the form code, it serves as a live documentation for the code under test.

# How writing testable code is possible?

## By following [Single responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle) in the code

And this means, your classes (and their methods) should not be taking more than one responsibility. This also enables writing unit test cases in isolation in an independent manner.

## By using [dependency injection and inversion of control](https://stackoverflow.com/questions/6550700/inversion-of-control-vs-dependency-injection) principles

This helps to use stubs and mocks for unit testing. I will explain about this with code samples in detail in subsequent articles.

![Writing testable code](/assets/images/writing-testable-code-matters/Writing-testable-code.png)

## By naming the UI controls properly and setting their automation ID’s

This helps test automation frameworks like “[Coded UI Tests](https://docs.microsoft.com/en-us/visualstudio/test/use-ui-automation-to-test-your-code)” or “[TestStack.White](https://github.com/TestStack/White)” to detect UI controls with minimal efforts.

## Advice

Follow [Test Driven Development (TDD)](https://en.wikipedia.org/wiki/Test-driven_development), i.e. write your unit test cases first then write your code. We are doing this to make our life easier; to improve the [overall design and architecture of the system](https://simpleprogrammer.com/tdd-unit-testing/).

Avoid tight coupling of the classes, stay dependent on the interfaces.

Write lots of unit tests using choice of your favourite test framework such as MSTest, NUnit, xUnit etc. Writing unit test will require you to use mocking frameworks such as Moq, NMock, RhinoMocks, NInject etc.

Emulate the .NET framework provided file system, date time and other API’s and functionalities using frameworks such as “[SystemWrapper](https://github.com/jozefizso/SystemWrapper) or [System.IO.Abstractions](https://github.com/tathamoddie/System.IO.Abstractions)”.

The framework themselves does not matter, what matters most is willingness to make code testable and become a pro.

 

# Further reading and references

1. [Back to Basics: Why Unit Testing is Hard](https://simpleprogrammer.com/back-to-basics-why-unit-testing-is-hard/)
2. [Unit Testing and Automated Blackbox Testing](https://simpleprogrammer.com/back-to-basics-unit-testing-automated-blackbox-testing-and-conclusions/)
3. [30 Days of TDD: Day One – What is TDD and Why Should I Use It?](https://www.telerik.com/blogs/30-days-tdd-day-one-what-is-tdd)
4. [Unit Tests, How to Write Testable Code and Why it Matters](https://www.toptal.com/qa/how-to-write-testable-code-and-why-it-matters)
