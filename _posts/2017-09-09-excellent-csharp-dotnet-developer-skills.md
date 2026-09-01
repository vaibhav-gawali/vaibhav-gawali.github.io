---
title: "Skills of an excellent C# .NET developer"
date: 2017-09-09
categories: 
  - "dotnet"
  - "csharp"
tags: 
  - "net"
  - "csharp"
  - "dotnet"
image:
  path: "/assets/images/excellent-csharp-dotnet-developer-skills/Master_of_IDE.png"
redirect_from:
  - "/excellent-csharp-dotnet-developer-skills/"
  - "/excellent-csharp-dotnet-developer-skills"
---

In my opinion here are some skills of an excellent C# .NET developer, I suggest to grow and strive for excellence to become one of the such developer.

# He has 50000 foot view of C# language and .NET framework features

You must master the basics of C# and .NET framework. However there is no need to learn every feature provided by the language and framework. You should know your programming language and framework basics thoroughly and be aware of all the other features. There are only 24 hours in a day to spend, and one can’t learn everything in one go. So learning should happen gradually but in time bound manner.

Have 50000 foot view and get into details as and when necessary.

That means, you should know enough where you can apply knowledge and when you need, get into details and learn the functionalities in detail later on.

For example, you do not need to master all of the functionality LINQ queries upfront, there is so much to learn. You just need to know the basics of static extension methods and basic LINQ query syntax, and then later on as and when required you can enhance your knowledge as per need basis.

# He is master of the IDE

You must master Visual Studio or whatever IDE you use. This not only improves your productivity but also helps in building your reputation amongst your colleagues as a reputed developer.

Increase your productivity with following

1. Know all the required IDE shortcuts
2. Know all the features provided by IDE
3. Master how to search within code and files outside of the solution
4. Know how to use bookmarks
5. Know how to use and apply code snippets

\[caption id="attachment\_412" align="alignnone" width="688"\]![C# .NET developer skills : Master the IDE](/assets/images/excellent-csharp-dotnet-developer-skills/Master_of_IDE-1024x593.png) C# .NET developer skills : Master the IDE\[/caption\]

# He knows how to effectively test the code

Testing is lot harder than you think. I wonder how many developers actually thoroughly test the code they themselves have written. Writing automated VSTS test cases is an art, and one must master it, either write VSTS test cases to test your code or have some test app / UI test cases to test your code. I strongly suggest to write VSTS/NUNIT test cases as we can use automated testing to test the code going forward.

As the number of arguments to API increases, so does the complexity of the API increases exponentially.

And in the busy day (tea/coffee/chitchat/news/gossips/online shopping etc.) one might not find time to write VSTS test cases (or might not be able to write them effectively) or might forget few use cases to test manually.

Consider below sample API and find out how many test cases one must cover as part of unit testing:

```csharp
public int Add(string num1String, string num2String);
```

[Refer complete sample code here](#SampleCode)

|   ###### **Sr. No.**   |   ###### **Unit test cases to consider**   |
| --- | --- |
| 1 | num1String when empty, throws ArgumentException |
| 2 | num1String when null, throws ArgumentException |
| 3 | num2String when empty, throws ArgumentException |
| 4 | num2String when null, throws ArgumentException |
| 5 | num1String when invalid value, throws ArgumentException |
| 6 | num1String when greater than int.MaxValue, throws ArgumentException |
| 7 | num1String when less than int.MinValue, throws ArgumentException |
| 8 | num2String when invalid value, throws ArgumentException |
| 9 | num2String when greater than int.MaxValue, throws ArgumentException |
| 10 | num2String when less than int.MinValue, throws ArgumentException |
| 11 | When num1 + num2 result goes out of positive range (i.e. greater than int.MaxValue), throws OverflowException |
| 12 | When num1 + num2 result goes out of negative range (i.e. greater than int.MinValue), throws OverflowException |

# He knows how to add documentation in the code

Adding XML documentation comments not only helps other developers to understand your code, but also it helps you to understand your code later on when it is long forgotten. Documentation comments should be well written and easy to understand.

While adding code documentation consider below points –

1. Any decisions should be documented and links to external/internal site and/or bug/backlog tracking system should be added for reference purpose
2. Maintain internal code references as appropriate
3. Document what kind of exceptions are explicitly thrown by the API
4. Mention if there are any assumptions in the API code
5. Explain about each parameter and validations present in the API for that parameter
6. Provide any example code as and when necessary

[Refer sample code for documentation example](#SampleCode)

# [He knows how to handle error and exceptions in the code](https://vaibhavgawali.net/csharp-dotnet-exception-handling-best-practices/)

This is the area which most new developers need to excel at. I have seen that even senior developers lacking expertise in this area.

Ask below questions to yourself when writing code –

1. Do you need argument validation in public methods of class?
2. Find out possible permutation combinations of arguments and their inter-dependencies in class’s public methods that require complex checks. Do you need to raise any custom exception or just raising ArgumentException suffice the purpose?
3. If your data come from file(s) or from database, then do you need any sanity checks? What will you do if sanity check fails?
4. Do you raise .NET framework provided exceptions like Exception, FileNotFoundException, NullReferenceException that are intended to be raised only from within .NET framework?
5. Do you need to create new custom exception or exceptions provided by .NET Framework can be reused (like InvalidOperationException, ArgumentException, ArgumentOutOfRangeException etc.)?
6. Can you recover from any Exception that is being raised by any other external/your own code?
7. When will you need to catch and suppress generic exception? Do you really need to suppress generic Exception?
8. Can you just catch specific exception like ArgumentException, IOException etc. as per need?
9. In case you have created your own custom exception, why would you care to make it serializable?

# He knows how to debug the code in an effective manner

This is most needed and at times challenging skill. Debugging not only means using state of the art IDE to debug your code, it also means debugging production issues in an effective manner when no IDE is available.

I have seen people even struggling to debug code even with development environment with Visual Studio installed. Here is my suggestion to explore and know the areas for effective debugging –

1. Master your IDE (see earlier section on this)
2. Get to know about call stack window, thread window, immediate window, Locals window command window and the list goes on
3. QuickWatch and other watch windows are very helpful
4. Thoroughly know breakpoints (how to set breakpoints conditionally)
5. Understand the power of Exception settings
6. Know the modules window
7. Know how to do remote debugging with Visual Studio remote debugger (msvsmon.exe)
8. Explore System.Diagnostics namespace and find out which classes you can use for your purpose (my favorite classes are StopWatch, Process and Debugger)

Apart from dev environment below things are required for effective debugging –

1. Understanding of the requirements in detail
2. Understanding of the codebase on which you are working
3. Thorough understanding of the domain you are working on
4. Awareness about effective logging/tracing

Here are few queries to boost your thought process –

1. You need to resolve problem at customer location and you don’t have access to customer’s PC. What will you do?
2. In your company domain someone is facing issue with your app. You can access users PC, now what will you do?
3. You need to fix a defect and you have full access to development environment. What will you do?

# He is the master of writing log/trace statement in an effective manner

Writing trace statements in the code is fairly standard practice for on premises debugging. Probably not every project follows this, however I would recommend it nevertheless. Because none can replace it when it comes to solving problems at customer location.

See [code sample for reference.](#SampleCode)

Here are some questions to ask yourself before writing trace statements in code –

1. Should you write method arguments to trace statements? What are the pros and cons of this?
2. How do you differentiate when to use verbose, info, warning and error logging?
3. Where will you write logs? (in file / database or default trace listener)
4. Will you consider hard coded strings or using resource strings for logging?
5. Do you need date and time info into log?
6. Should you use .NET framework provided diagnostic Trace API’s or any other logging framework such as log4net?

# He is master of designing class, interface API’s for other developers to use

Defining interface, class and their properties and methods with proper name is important. Other developers who will use these should be able to easily guess/understand the purpose.

This can be only achieved by practice. Few questions to ask yourself –

1. Which names you will choose for class, interface, properties and method names? Can they resonate the intentions clearly?
2. Do you apply SOLID principles while designing the API’s?
3. Do you enforce SOLID principles by design?
4. No design is perfect at start. Do you refine the design as you discover new challenges?
5. Do you do design reviews?

Here is one good book that I can recommend - "[.NET framework design guidelines](https://vaibhavgawali.net/recommends/net-framework-design-guidelines/)"

# He quickly understands and interprets code written by other developers

This is the most required skill nowadays, since almost every project has some form of pre-written or legacy code that needs to be maintained, to either add new requirements or to fix defects in the code.

You need to spend some time understanding existing code. Yes, there are challenges however this is the most important part.

You must understand the domain and requirements first in order to be able to understand and know codebase.

Sometimes you will need to add trace statements and sometimes just debugging the code is sufficient.

# He can go to the extra mile to integrate his code with other technologies

Sometimes there is a need to integrate code written in C# / .NET into other technologies such as VC++, COM, JAVA or legacy VB6. Someone needs to do this and this requires some level of understanding of the technology in which integration needs to be done.

You must be willing to take the step forward and learn the new things to make this happen. Trust me, if you do this, you will not only feel satisfied but also grow your knowledge base; and when you grow there is progress.

# He knows the build and deployment/installation environment

Get familiar with your build and deployment/installation environment. Once this is done, you should be able to solve additional issues of build/deployment/installation. And more issues you solve, more your reputation will rise.

Here are some questions to boost your thought process –

1. Do you know how to write MSBuild scripts?
2. Can you automate tasks with any type of scripts such as MSBuild script, batch files and Jenkins etc.?
3. Will you learn new skills required for the build/deployment/installation?

# He is master of writing multi-threaded applications

Writing multi-threaded apps is not a simple task. And once you master this, I bet you can effectively do any other type of coding that can be done in C# and .NET.

Here are some questions to boost your thought process –

1. Why do you need thread synchronization?
2. Do you know how to do thread synchronization?
3. Which C# language features you can use for thread synchronization?
4. Which classes from .NET framework are useful for thread synchronization?

# He can create effective proposals

A developer’s job is not only to write code but also to writing effective proposals for various purposes such as design of an interface/class or to put forward his idea about how to cater to specific requirement.

No one is going to listen to you unless you know how to make them listen to you. Otherwise you will just drift apart and write code as per what others think a good design is.

I admit that mastering this skill is not so easy, and it will take time and a quite good amount of effort. Do whatever it takes, and master this skill.

Here are some questions to boost your thought process –

1. Do you consider pros and cons for the design or specific way of handling the requirement?
2. Can you write summary of the proposal?
3. Will you add sequence diagram / flow charts in your proposals?
4. Do you ask questions to understand requirements / design before you propose anything?
5. How will you document proposals and their multiple versions?

# He can do [effective code reviews](https://vaibhavgawali.net/observations-from-code-reviews-and-why-they-are-important/)

Great C# .NET developer skills include doing effective code reviews of peers. Doing code reviews not only increases understanding of the code base but also improves feedback and communications skills.

# Conclusion:

One cannot become great developer overnight, it need practice and patience and experience. To become a great C# .NET developer, you will not only need to pay attention to acquire the new Skills but also need to practice, practice and practice.

Here is my final advice - [Be so good that they can't ignore you](https://vaibhavgawali.net/recommends/good-cant-ignore/) (a book by Cal  Newport).

 

# Sample code:

 

```csharp
namespace Math
{
    /// <summary>
    /// This class provides basic Math API's for add operation for number values in string form.
    /// Requirement details can be found at https://vaibhavgawali.net
    /// </summary>
    class Adder
    {
        static TraceSwitch s_traceSwitch = new TraceSwitch("Default", "Default", "On");

        /// <summary>
        /// This API adds the two numbers that are provided in the string format.
        /// Numbers in string format are converted to integer and any conversion errors are re-thrown.
        /// <para><c>
        /// Adder a = new Adder();
        /// int sum = a.Add("123", "321"); //Acceptable
        /// sum = a.Add("", "321"); //Throws ArgumentException
        /// sum = a.Add("123", ""); //Throws ArgumentException
        /// sum = a.Add("12345678123456789", "123"); //Throws ArgumentException
        /// </c></para>
        /// </summary>
        /// <param name="num1String">This is string containing number.
        /// Null or empty string is not allowed. An <typeparamref name="System.ArgumentException"/> is raised.</param>
        /// <param name="num2String"></param>
        /// <returns></returns>
        /// <exception cref="ArgumentException">If <paramref name="num1String"/> or <paramref name="num2String"/> is <c>null or empty</c>.</exception>
        /// <exception cref="OverflowException">When addition of <paramref name="num1String"/> and <paramref name="num2String"/> is <c>does not fit into int value</c>.</exception>
        /// <example>
        /// <code>Adder a = new Adder();
        /// int sum = a.Add("123", "321"); //Acceptable
        /// sum = a.Add("", "321"); //Throws ArgumentException
        /// sum = a.Add("123", ""); //Throws ArgumentException
        /// sum = a.Add("12345678123456789", "123"); //Throws ArgumentException
        /// </code>
        /// </example>
        public int Add(string num1String, string num2String)
        {
            if (s_traceSwitch.TraceVerbose)
            {
                Trace.WriteLine(((FormattableString) $"{nameof(Adder)}.{nameof(Add)}: num1String = {num1String}, num2String = {num2String}").ToString(CultureInfo.InvariantCulture));
            }
            ThrowArgumentExceptionIfNullOrEmpty(num1String, nameof(num1String), "First number cannot be null or empty.");
            ThrowArgumentExceptionIfNullOrEmpty(num1String, nameof(num2String), "Second number cannot be null or empty.");
            int result, num1, num2;
            num1 = ConvertToNumber(num1String, nameof(num1String), "String to int conversion failed for first number.");
            num2 = ConvertToNumber(num2String, nameof(num2String), "String to int conversion failed for second number.");
            checked
            {
                result = num1 + num2;
            }
            if (s_traceSwitch.TraceVerbose)
            {
                Trace.WriteLine(((FormattableString)$"{nameof(Adder)}.{nameof(Add)}: {num1String} + {num2String} = {result}").ToString(CultureInfo.InvariantCulture));
            }
            return result;
        }

        /// <summary>
        /// Validates the string argument and throws an exception with provided error message when string to validate is null or empty.
        /// </summary>
        /// <param name="stringToValidate">This is the string to validate for <c>null</c> or <c>empty</c>.</param>
        /// <param name="argName">Name of the argument which needs to be added as <c>paramName</c> in <c>ArgumentException</c>.</param>
        /// <param name="conversionFailureErrorMessage">Error message that needs to be used while raising <c>ArgumentException</c>.</param>
        /// <exception cref="ArgumentException">When <paramref name="stringToValidate"/> is <c>null or empty</c>.</exception>
        private static void ThrowArgumentExceptionIfNullOrEmpty(string stringToValidate, string argName, string conversionFailureErrorMessage)
        {
            if (s_traceSwitch.TraceVerbose)
            {
                Trace.WriteLine(((FormattableString)$"{nameof(Adder)}.{nameof(ThrowArgumentExceptionIfNullOrEmpty)}: stringToValidate = {stringToValidate}, argName = {argName}").ToString(CultureInfo.InvariantCulture));
            }

            if (string.IsNullOrEmpty(stringToValidate))
            {
                if (s_traceSwitch.TraceError)
                {
                    Trace.WriteLine(((FormattableString)$"{nameof(Adder)}.{nameof(ThrowArgumentExceptionIfNullOrEmpty)}: Null or empty validation failed for argName {argName}. Error: {conversionFailureErrorMessage}").ToString(CultureInfo.InvariantCulture));
                }
                throw new ArgumentException(conversionFailureErrorMessage, argName);
            }
        }

        /// <summary>
        /// This method converts given string to integer format using InvariantCulture as base for any number style.
        /// </summary>
        /// <param name="numberString">String that needs to be converted to integer.</param>
        /// <param name="argName">Name of the argument which needs to be added as <c>paramName</c> in <c>ArgumentException</c>.</param>
        /// <param name="conversionFailureErrorMessage">This error message is used to raise an ArgumentException.</param>
        /// <returns>Converted integer number from provided string value.</returns>
        /// <exception cref="ArgumentException">When int.TryParse fails for <paramref name="numberString"/>.</exception>
        private static int ConvertToNumber(string numberString, string argName, string conversionFailureErrorMessage)
        {
            if (s_traceSwitch.TraceVerbose)
            {
                Trace.WriteLine(((FormattableString)$"{nameof(Adder)}.{nameof(ConvertToNumber)}: numberString = {numberString}").ToString(CultureInfo.InvariantCulture));
            }
            int number;
            if (false == int.TryParse(numberString, NumberStyles.Any, CultureInfo.InvariantCulture, out number))
            {
                if (s_traceSwitch.TraceError)
                {
                    Trace.WriteLine(((FormattableString)$"{nameof(Adder)}.{nameof(ConvertToNumber)}: int.TryParse failed for numberString = {numberString}, argName {argName}. Error: {conversionFailureErrorMessage}").ToString(CultureInfo.InvariantCulture));
                }
                throw new ArgumentException(conversionFailureErrorMessage, nameof(numberString));
            }

            return number;
        }            
    }
}
```
