---
title: "Localization, Globalization and Internalization in .NET for Windows Desktop applications"
date: 2018-04-07
categories: 
  - "dotnet"
  - "internationalization"
tags: 
  - "net"
  - "c"
  - "csharp"
  - "dotnet"
  - "globalization"
  - "internationalization"
  - "loalization"
coverImage: "Globalization-Internationalization-Localization.png"
---

Globalization of software cannot be a afterthought, [an expert C# developer](https://vaibhavgawali.net/excellent-csharp-dotnet-developer-skills/) will always pay attention to globalization. Globalization of the .NET applications is made very easy by Microsoft's .NET team. This covers following things –

1. Terminologies – Localization, Globalization and Internationalization
2. Things to consider for making application world ready
3. Code level considerations

Let’s get started.

# Terminologies – Localization, Globalization and Internalization

## Localization:

Localization is the process of translating an application's resources into localized versions for each culture that the application will support.

Examples:

- Translation of resource strings for specific culture/language that are supported by application.
- Culture specific localized images used in the application.

## Globalization:

It is the process of designing and developing a world-ready app that supports localized interfaces and regional data for users in multiple cultures. And this also means that application can handle things like date time formats, currency, string comparison and sorting etc.

Examples:

1. Displaying date time to user in culture specific format
2. Persisting date and time info in culture insensitive manner
3. Currency conversion and displaying currency values
4. A message box displaying message string to user, shows message in the language as per the Windows OS language. (In this case message string gets replaced at runtime with localized version of the language)

## Internationalization

It is the process of localizing and globalizing application, and hence it is super-set of both.

![Globalization-Internationalization-Localization](/assets/images/localization-globalization-and-internalization-in-net-for-windows-desktop-applications/Globalization-Internationalization-Localization.png)

# Things to consider for making application world ready

There are certain rules that we need follow to allow internationalization of our application. Below are some of the areas that we must pay attention to when we write code to support globalization in our application

1. Use resource strings for display purpose
2. Persist/serialize numbers using invariant culture and display using desired culture
3. Persist/serialize date and time using invariant culture and display using desired culture
4. Number stored in one currency cannot be directly shown as different currency, and it must be converted by applying appropriate currency conversion rules
5. Decide which exception error messages needs to be localized and which ones not, as thumb rule, internal/logic errors related messages need not be localized
6. Logging/tracing should be done only in the language that developer understands (usually English, you don’t want to debug onsite issues with Chinese trace unless it is your mother tongue)

# Code level considerations

At code level, we need to ensure that globalization support related changes are in place so that all types of cultures can be supported. Here are some of the tips that you should do for globalization of an application –

Declare [AssemblyCulture attribute](https://msdn.microsoft.com/en-us/library/system.reflection.assemblycultureattribute\(v=vs.110\).aspx) at assembly level for main assembly (by default this is added in the project by Visual Studio IDE).

\[assembly:AssemblyCulture("")\]

Declare [NeutralResourcesLanguage attribute](https://msdn.microsoft.com/query/dev14.query?appId=Dev14IDEF1&l=EN-US&k=k\(System.Resources.NeutralResourcesLanguageAttribute\);k\(TargetFrameworkMoniker-.NETFramework,Version%3Dv4.5\);k\(DevLang-csharp\)&rd=true) at assembly level to specify default culture of the assembly. This improves performance if resources are present in the assembly. \[assembly:NeutralResourcesLanguage("en-US")\]

All display strings (optionally images) presented to the user should come from Resources (i.e. from ResourceManger).

Run Microsoft provided globalization code analysis rules, and resolve all warnings related to that. Also consider running these rules during build (by enabling these setting at project level) and treat these rules as errors instead of warnings.

## For numeric-string-numeric conversion:

Use overloaded ToString method of numeric types that accepts ‘[IFormatProvider](https://msdn.microsoft.com/query/dev14.query?appId=Dev14IDEF1&l=EN-US&k=k\(System.IFormatProvider\);k\(TargetFrameworkMoniker-.NETFramework,Version%3Dv4.5\);k\(DevLang-csharp\)&rd=true)’ object and pass on CultureInfo object (pass InvariantCulture to persist/serialize numeric values).

Use TryParse method and pass InvariantCulture while de-serializing.

## Useful Classes/Namespaces

[System.Resources](https://msdn.microsoft.com/en-us/library/system.resources\(v=vs.110\).aspx)

[System.Globalization](https://msdn.microsoft.com/en-us/library/system.globalization\(v=vs.110\).aspx)

## WinForms app

Windows forms localization is achieved by following –

For each form, set Localizable property of Windows Form to true. This auto generates form specific default resource file & uses ‘ComponentResourceManager’ to apply resources at runtime.

A code sample will be added in part – 2 of this series.

## WPF app

You can bind text resources in the XAML to static properties of designed generated resource class as shown below –

“Title="{x:Static prop:Resources.MainWindowTitle}"”

As a guideline keep enough space between UI controls so that culture specific text and images can be accommodated.

A code sample will be added in part – 2 of this series.

## Console app

Old version of .NET Frameworks (prior to .NET 4.5) lacked support of [UTF-16 encoding for Console character display](https://msdn.microsoft.com/en-us/library/system.console.outputencoding\(v=vs.110\).aspx). This also requires TrueType font to be set on Console itself for proper display of Unicode characters. (As of writing this article I was not able to display Indic characters onto the Console)

# Useful Tools

## [Resource File Generator (resgen.exe)](https://docs.microsoft.com/en-us/dotnet/framework/tools/resgen-exe-resource-file-generator)

The Resource File Generator (Resgen.exe) converts text (.txt or .restext) files and XML-based resource format (.resx) files to common language runtime binary (.resources) files that can be embedded in a runtime binary executable or satellite assembly.

## [Windows Forms Resource Editor (Winres.exe)](https://docs.microsoft.com/en-us/dotnet/framework/tools/winres-exe-windows-forms-resource-editor)

This is an alternative to Visual Studio IDE that just focuses on resource localization of Windows Forms. Winres.exe, is a visual layout tool that helps localization experts localize Windows Forms user interface (UI) resources used by forms.

Winres.exe is the recommended tool to use if localization will be done by third-party localizers. Because Winres.exe is a localization tool only, it allows for a cleaner separation of an application's code from the forms to be localized, which is more practical for managing large projects.

## References:

Here are some good articles I have come across, these should help to you as well –

1. [Globalization on Microsoft docs](https://docs.microsoft.com/en-us/dotnet/standard/globalization-localization/globalization)
2. [Globalization localization](https://docs.microsoft.com/en-us/dotnet/standard/globalization-localization/globalization)
3. [Localizability review](https://docs.microsoft.com/en-us/dotnet/standard/globalization-localization/localizability-review)
4. [Integer to string using ToString method and format specifier](https://msdn.microsoft.com/en-us/library/d830955a\(v=vs.110\).aspx)
5. [Standard numeric format string](https://docs.microsoft.com/en-us/dotnet/standard/base-types/standard-numeric-format-strings)
