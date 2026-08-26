---
title: "Observations from code reviews and why they are important"
date: 2017-08-14
categories: 
  - "dotnet"
tags: 
  - "net"
  - "code"
  - "codereview"
  - "dotnet"
  - "review"
---

I work on a C# and .NET based technology and I would like to share my experience on why code review is an important activity in the project.

* * *

### [What is code review](https://en.wikipedia.org/wiki/Code_review)? (From Wikipedia)

> Code review is systematic examination (sometimes referred to as peer review) of computer source code. It is intended to find mistakes overlooked in the initial development phase, improving the overall quality of software. Reviews are done in various forms such as pair programming, informal walkthroughs, and formal inspections.

* * *

\[caption id="" align="alignnone" width="623"\]![](/assets/images/observations-from-code-reviews-and-why-they-are-important/AAEAAQAAAAAAAAx8AAAAJDhlNzZjMmJhLWM1Y2EtNGNkNy1iODJkLWMyN2YxMmM5YTM4Nw.png) Code Review\[/caption\]

.

* * *

### Below are some common areas where I have found that teams can improve on at higher level –

Below are some common areas where I have found that teams can improve on at higher level –

1. Running code analysis on the code before check-in of even single line of code
2. Finding out comprehensive list of unit test cases for which code should be tested (if list is big then sampling should be done)
3. Missing unit test cases
4. Doing self-review of code before check-in to source control
5. Adding proper code check-in comments
6. Proper error handling
7. Using logging/tracing properly
8. Application of SOLID principles on the code
9. Pay attention to performance of the code
10. Memory leaks (yes its possible in .NET as well)
11. Choosing good names in the code
12. Security aspects in the code

\[caption id="" align="alignnone" width="600"\]![](/assets/images/observations-from-code-reviews-and-why-they-are-important/AAEAAQAAAAAAAAzdAAAAJDRiMWQyNmYwLTc5YjYtNDQ2Ni1hNmE5LWI5MGRhMmI3Nzg4Yw.jpg) Programmers Hardest Tasks\[/caption\]

## Running code analysis on the code before check-in of single line of code

Although this is a common sense, still no one pays attention to this area. And here could be probable reasons for this –

1. Code is already written by someone else and currently being maintained. Now, no one dares to run code analysis and fix issues reported by “Visual Studio Code Analyzer”
2. Fresher or junior developer not aware of this feature of Visual Studio
3. This activity is not listed in the project activities or guidelines

Here are some solutions to above mentioned problems –

Initially suppress all warnings in the C# project in the existing code using “Run Code Analysis and Suppress Active Issues” option. This creates ‘GlobalSuppressions.cs’ file and suppresses all existing warnings. Now you should be able to at least start with running code analysis on code you add/write in the component being maintained

Include this in the induction plan of the project that every newcomer developer must undergo. This will not only create awareness in the new developers but also they will understand the importance of this activity.

PM or senior developers must update guidelines or practices followed in the project and enforce this practice; no exceptions allowed here.

I think it is good practice to enforce this by enabling C# project build setting “Treat warnings as error” to “All” as well along with enabling all code analysis rules for the solution or project.

[This stack overflow thread explains about how to treat code analysis ruleset warnings as errors](https://stackoverflow.com/questions/14366181/treat-warnings-as-errors-has-no-effect).

\[caption id="" align="alignnone" width="657"\]![](/assets/images/observations-from-code-reviews-and-why-they-are-important/AAEAAQAAAAAAAAsKAAAAJDJjOWM0ODJlLTdlMTctNDllMC1hMjNkLTlhZDU3NTAzM2U4OA.png) Enable code Analysis\[/caption\]

 

## Finding out comprehensive list of unit test cases for which code should be tested (if list is big then sampling should be done)

Unit testing is an area which most developer tends to fail to access properly. Generally most common use cases are covered and corner cases are not considered at all.

 

How to address this? – Take pen and paper and try to come up with an approach to break the code. Think and try to come up with approaches to deal with cases that break your logic.

Write VSTS test cases for the component. I have seen that sometimes developers just either do not write any VSTS test cases or just write these for the sake of it. Junior developers need some guidance here, however once the process is known then it’s very easy.

VSTS test cases must be integrated into automated build process to ensure code stability.

I have seen that some shabby developers that leave it up to test team to cover even most of unit testing part of it. These are the ones who knowingly or unknowingly spoil the team spirit, work environment and ethics. Immediate steps are needed to deal with such incidences.

## Missing unit test cases

You may probably wonder that this has been covered already, however there lies a bitter truth – there are no unit test cases at all.

Especially this is the case with legacy code and it becomes very tedious to write test cases for legacy code. This is a tricky scenario and needs to be dealt on case by case basis; there is no magic formula for this.

Sometimes tight deadlines are the culprit and sometimes not adhering to guidelines and good practices.

First case can be dealt easily by adding technical debt that team must work on once high pressure situation is over. However we must pay attention to the developers who think “I just need to write code, test team has to test it, and it’s not my responsibility”. These cases cannot be ignored and must be dealt seriously.

## Doing self-review of code before check-in to source control

I have seen developers who do not pay attention to this activity; novices to experts. This is the most important activity one must follow without fail and here’s why –

This is the last minute check for the code. Perhaps you may have missed one if condition for some corner case or you have earlier deferred writing code summary comments.

Now is the time to act on all earlier deferred activities.

Is your code understandable by someone else? Can someone easily maintain it?

If answer to these questions is NO, then probably you need one more level of refactoring in the code. Act on it before you check-in the code.

## Adding proper code check-in comments

Sadly this is the most neglected area by developers. Even though version control system provides nice way of providing code check-in comments developers just ignore it. When things go wrong and when we want to understand why certain things are done in particular manner without proper check-in comments it becomes very difficult to get to the root cause.

Do I want others to compare modified all code and then let them figure out what has been done? What if others do the same thing to me?

Here are some examples of bad check-in comments (number 1 is blank):

2. Fixed D-12345
3. Fixed Object reference error
4. Fixed defect D-12345: Object reference error when clicked on about box button

No wonder those developers who maintain code written by others feel like having address of the developer who wrote the code earlier; you can easily guess, why.

Example of good check-in comment:

Fixed D-12345: Object reference error when clicked on about box button

Root cause: Registry key is always assumed to be present, there was missing null check.

Done below changes in ‘SplashScreen’ component:

1. Added null checks for missing registry keys
2. Displayed <#Error> for missing copyright year (& et al values that are read from registry)

## [Proper error handling](https://vaibhavgawali.net/csharp-dotnet-exception-handling-best-practices/)

This is the most important area and still the most neglected one, even the most experienced developers don’t pay much attention here. Surprised? Here’s my observation –

1. Missing argument checks in public methods. This can be easy to fix, like adding various checks on method arguments such as null check, out of range check for numeric values. Based on these checks an appropriate exception can be raised such as ArgumentNullException, ArgumentException etc.
2. Missing validation of data passed to method. Sometimes a complex object is passed to method and it’s not validated at all for integrity. Ensuring correctness of data and raising appropriate exception with proper error message helps in the debugging.
3. Not considering external factors affecting logic of the code and handling it in proper manner. External factors may affect code and these should be considered; example: missing files or registry entries on which code depends.
4. Destroying stack trace of an exception with statements such as “throw ex;”, “throw new Exception(‘<Error message>’)”. Stack trace of an exception must be preserved at all cost unless it’s done deliberately with specific purpose.
5. Generic “Exception” is raised instead of specific exception. This is done despite presence of explicit guidelines from Microsoft.
6. Suppressing exception without notifying users. I have recently seen, a newly written GUI not properly responding to user actions or shutting down without even giving any error message. This frustrated me a lot, I then debugged and found that at many places Exceptions were just caught and silently ignored; GUI was closed in case of any errors during initialization. (Thanks to no code reviews and zero testing by test team because of release pressure and poor management by team lead)

## Using logging/tracing properly

Logging is an important part of any enterprise application. And yet this is not used effectively and efficiently.

Here are some questions for you –

Do you log trace messages?

Which one of the following statements you consider will help in offline debugging?

logger.Error(exception.Message);

logger.Error(exception);

if(logger.ErrorEnabled) { logger.ErrorFormat(“Failed to read registry key {0}. #Exception: {1}”, regKeyPath, exception); }

Will you write localized resource strings into log or always log an English string? (Unless you can debug with Chinese trace)

Do you log additional info into trace that can be useful for offline debugging purpose?

Do you mix and match Debug, Info, Warn and Error kind of trace messages?

Do you consider not concatenating trace message strings when logging is disabled?

## Application of [SOLID principles](https://en.wikipedia.org/wiki/SOLID_\(object-oriented_design\)) on the code

I have seen senior most developers (whose code has least defects) still writing 300+ lines of methods (1000+ in some cases). This includes nested for, foreach, if statements with error handling code. No wonder, if junior developers take the same path.

May be its time to learn SOLID principles, go back to roots and learn SOLID principles (& oops) all over again.

If you can apply below principles, then code you write not only becomes maintainable but also you earn respect as someone who is role model of others who deserves serious respect from fellow team members.

S – [Single Responsibility Principle](https://en.wikipedia.org/wiki/Single_responsibility_principle)

O – [Open & Closed principle](https://en.wikipedia.org/wiki/Open/closed_principle)

L – [Liskov’s Substitution Principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle)

I – [Interface Segregation Principle](https://en.wikipedia.org/wiki/Interface_segregation_principle)

D – [Dependency Inversion Principle](https://en.wikipedia.org/wiki/Dependency_inversion_principle)

## Pay attention to performance of the code

Performance is an implicit feature of an application and must be given attention right from the start and yet this is an ignored area. Tiny steps to improve performance add up and increase overall throughput of the system.

Sometimes I have seen that exception handling is used in most common scenarios.

For example: Why can’t I use “int.TryParse()” method instead of “Convert.ToInt()” and then catching an Exception about conversion.

It also needs additional efforts to measure performance of an applications. The brand new Visual Studio IDE allows to monitor and measure CPU or memory performance. And there are additional tools such as ANTS profiler are available as well.

## Memory leaks (yes its possible in .NET as well)

In our project we deal with COM components from managed code. And hence it is possible to leak memory or handles in this scenario. Once we found that COM component was not releasing opened file handle because developer did not care to call an appropriate API on COM object to release the file.

It is also possible to leak memory in managed code in areas such as event handlers that are never unregistered or some static member that is not set to null. These need careful code inspection and has its own challenges.

Following guidelines should help:

1. Always dispose objects once they are no longer needed
2. Release COM objects using Marshal.ReleaseComObject API
3. Release opened files or registry keys etc. or any opened handles once they are no longer needed

## Choosing good names in the code

Mostly classes, member variables and methods are not named properly. And for most of us this is the lacking area to which we think there is no real value in the improvement.

WRONG, we must pay attention and improve upon naming things. This makes code readable and maintainable.

Which of the below code statement seems better?

for(int i=0; I < length1; i++) { … }

for(int dataTypeIndex=0; dataTypeIndex < dataTypesCount; dataTypeIndex++) { … }

Perhaps you can refer article “[How to Choose Good Names in Code](https://simpleprogrammer.com/2017/02/22/choose-good-names-code/)” for more clarity on this.

## Security aspects in the code

Ouch! I don’t know what is meant by this. My code produces exe and it is not readable by user, then why should I care? Do you mean I really need to pay attention here?

Above is my response when I was a brand new coder.

Let me share my own experience of security breach by my smart fellow developer. Once we were working on one critical important feature of the release, and we had to create Windows user with admin privilege. Developer working on the feature, hard coded the password in the code. My another smart fellow developer knew this fact and hacked into the PC’s where software was installed since he knew the local user’s hard coded password. And he was gracious enough to tell this. Next thing we did is to use SecureString and then randomly generating the password for the Windows user.

You can probably refer “[5 Security Concepts Every Developer Should Understand](https://simpleprogrammer.com/2017/04/19/5-security-concepts/)” for better understanding of the security topic.

## Conclusion:

Writing good and maintainable code is a responsibility of software developer and code review process helps to achieve this goal.

I may have hurt someone’s sentiments and this was my original intention. However, if this makes you better developer then why not take some actionable steps now to make your code a masterpiece.

Perhaps “Code Reviewer” may get overwhelmed with all these kind of reviews he must perform. Why not delegate some of these tedious or mundane tasks to code analyzer tools?

[Visit this Github page that lists down some awesome static code analysis tools](https://github.com/mre/awesome-static-analysis#c).

Here are some good articles I have come across for code reviews, these should help you and your team to keep motivated about code review activities.

1. [Code review guidelines](https://www.codeproject.com/Articles/524235/Codeplusreviewplusguidelines)
2. [Reduce Bad Code with Code Reviews](http://www.dotnetcurry.com/software-gardening/1351/types-of-code-review-benefits)
3. [Why Agile Is Dead: Long Live The Code Review!](https://simpleprogrammer.com/2017/02/17/agile-is-dead-code-review/)
4. [Don’t Snub the Code Review](https://simpleprogrammer.com/2010/06/09/dont-snub-the-code-review/)
5. [Hunting Down The Mythical High Quality Code](https://simpleprogrammer.com/2016/11/04/hunting-mythical-high-quality-code/)
6. [Security From the Start](https://simpleprogrammer.com/2017/02/03/security-from-the-start/)

Happy Coding!!!

**Vaibhav M. Gawali**

Passionate .NET developer, a #10Xer, #productivity maniac, #Agile-list, father & husband who loves to solve difficult problems related to software development.

This article was [originally published at LinkedIn](https://www.linkedin.com/pulse/observations-from-code-reviews-why-important-vaibhav-gawali).
