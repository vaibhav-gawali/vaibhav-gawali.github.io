---
title: "Are you doing Effective Testing?"
date: 2018-03-04
categories: 
  - "dotnet"
  - "testing"
tags: 
  - "testing"
  - "unit-testing"
---

Have you ever faced a challenge of timely delivery with well tested software? Welcome, join the club, you are not alone out there who is facing this challenge.

Most of the time, it is very difficult to come up with a good test plan that can cover every possible combination of inputs and external conditions and still meet the software release deadlines. And hence effective testing is one of the challenges we face during software development life cycle.

In this post I am trying to convey an important message about – testing software effectively with well tested deliverables, with concrete example of “Login Dialog”.

However, before I start on this, lets back-up and revise our intention for effective testing.

# Why should we care for Effective Testing?

Well, every stakeholder can have different answer to this question.

Software developer: My code must be defect free, I must be known as the one who always delivers quality code.

Tester: I need my next promotion, so I must showcase my skills of how much effectively I can test.

Project Manager/Product Owner/Scrum Master/Company: We need repeat business by delivering quality product to the customer.

Customer: The software I am using must work as advertised. I cannot tolerate any issues that hampers my work.

# Who is responsible for effective testing?

Of course, tester is always responsible. In fact, he is the gate keeper who does all the dirty work which sometimes developer is not willing to do.

Product quality is responsibility of entire team, and hence testing is a team effort.

> “You cannot have the mindset that QA will find the bugs in your code. Instead, you should absolutely make it your responsibility to find and fix the bugs before your code goes to testing.” - John Sonmez

Project manager/Product owner/Scrum Master: Must ensure that requirements conveyed are the ones which needs to be implemented. They validate and re-validate whether deliverable's are of good quality.

# What is involved in Effective Testing?

## Clarity in requirements

This is must, without clarity in requirements it is not possible to deliver quality product that customer can use. Agile methodologies such as Scrum enforces this as part of backlog grooming, however if team is actually doing tailored Agile approach then it is possible that developers work on features without absolute clarity and this might lead to issues later on. Issues may include rigid and inflexible software because of bad design, re-work on features and defects in the system.

## Maximum test coverage of functionality in minimum time

There is always pressure to release the software as soon as possible. Hence in limited time team needs to achieve maximum test coverage in the minimum possible time. Here are some ways to maximize test coverage –

### Guidelines

1. Prepare test data/input data.
2. Consider maximum possible permutations/combinations of required inputs, however some combinations follow similar code paths, hence some of the combinations can be skipped for testing. Always pick the most stringent inputs.
3. Consider supported test environments. (Examples: Windows 10, Windows 7, Red-Hat Linux etc.)
4. Find out worst case scenarios. (Example: Server connectivity lost in the middle of data transfer)
5. Find out best case scenarios. (Example: All inputs are favorable)
6. Find out happy path workflows. (Example: Login dialog being shown for multiple scenarios and executing code of multiple modules working cohesively for user actions)
7. Find out external conditions impacting happy path workflows. (Examples: LDAP server unavailable)

### Crystal clear test strategy

This requires multiple strategies and you cannot rely on one or two testing strategies. Here are some minimum recommendations –

##### Unit testing:

This is the best effort from developer’s side to ensure that newly written code does what it is expected to do, and how the code will react to external impacting factors that may or may not have favorable conditions.

I personally like to have fully automated unit test cases, however for legacy code (with lots of dependencies) for which automated tests can’t be written there must be some plan to perform basic unit testing.

When TDD approach is followed using unit testing frameworks (such as MSTest, NUnit, xUnit et al), this is the most powerful way of development.

##### Integration testing

It is must to test multiple independent units of system working in cohesive manner.

Examples:

1. Authentication module used by login dialog needs to be tested with “Authorization Module”
2. Login Dialog is required to re-authenticate user before data is submitted

\[caption id="attachment\_482" align="aligncenter" width="457"\]![Modules in the system](/assets/images/are-you-doing-effective-testing/Modules-in-the-system.png) Integration Testing of modules in the system\[/caption\]

##### Workflow testing

Test end-to-end workflow of end-user scenarios. (And this may be called a system testing)

Examples:

1. Administrator logs into the system and approves financial data submitted by Accountant of the company.
2. POS operator logs into the system and for each customer in the queue prepares bill of purchased goods, applies any coupons for discount and accepts payment from customer and generates the bill.

##### **Performance testing**

Identify areas in your software where performance testing is required, and define your goal in this area.

Examples:

1. System can handle 1000 login requests per second
2. System can process 1 GB data per second

### Technical reviews

It is absolutely must to perform technical reviews. These are far cheaper and more effective than testing if done properly.

**Design reviews:** When we do design review, we not only validate from requirements standpoint, but also for future extensibility point of view. And this helps a lot as we progress from one version of software to another.

**Code reviews:** These can catch potential issues sooner before test team even gets the deliverables to test. And I have written [another post that detailed out this approach](https://vaibhavgawali.net/observations-from-code-reviews-and-why-they-are-important/).

**Test case reviews:** Whether it is automated unit test case, manual test case document or any other type of test case (Coded UI, Specflow etc.). Often this step is skipped and some of the important aspects are always missed.

### **Documentation of Results**

**Documentation of expected results:** In Scrum or Kanban type of project ideally this should get recorded as part of acceptance criteria. However, when functionality is complex, there may be additional aspects that needs to be documented. Perhaps these could be implicit requirements that were not captured in the backlogs acceptance criteria.

**Documentation of Actual results:** Professional teams know the importance of actual results documentation. And if you are using JIRA or VersionOne like tools then you may be already doing this. Just note that don’t skip this one.

> Our main focus is on requirements, however we should also verify what application is not intended to do.

 

# The Inverted Testing Pyramid

![](/assets/images/are-you-doing-effective-testing/The-Inverted-Test-Pyramid.png)

# Cost of Defect at Various Stages

[![](/assets/images/are-you-doing-effective-testing/Cost-of-defect-at-various-stages.png)](http://www.agilemodeling.com/essays/costOfChange.htm)

\*\* This image belong to the rightful author(s)

# Guidelines To Write Test Cases

1. Intelligently choose the relatively few test cases
2. Cover all requirements and features defined in the requirements specifications
3. Test cases should not be redundant
4. Maximum focus on scenarios that users are likely to encounter in practice
5. Analyze all points at which data enters the system and look for ways to attack it
6. Separate out workflow test cases from functionality specific test cases
7. Test case should have references or inbuilt section of unsupported scenarios (or have these listed in the backlog)
8. Consider integration with 3rd party components
9. Come up with list of external integration points

# Guidelines for Developers

1. Write automated unit tests (for new components)
2. Keep automated unit tests updated (for old components)
3. Run automated unit tests as part of build activity.
4. Test code should be treated as production code
5. Leverage knowledge of code to perform - White Box Testing

# Effective Testing Example for Login Dialog Use Case

![](/assets/images/are-you-doing-effective-testing/Login-Dialog.png)

## Detailed out Acceptance Criteria of the Backlog

Below login dialog use cases will be supported on Windows 10 (64 and 32 bit) as well as Windows 7 (64 and 32 bit) OS.

The login dialog internally uses Windows OS inbuilt API's to login as a local user or as domain user.

| **Sr. No.** | **Use Case** | **Remember user name** | **Expected behavior** |
| --- | --- | --- | --- |
| 1 | User cancels login | Checked | Dialog closes. <Save entered user name? Is this really a requirement? - Is this documented?> |
| 2 | User cancels login | Unchecked | Dialog closes. <Save entered user name? Is this really a requirement? - Is this documented?> |
| 3 | User enters valid credentials | Checked | Login happens. User name is remembered for next time use. |
| 4 | User enters valid credentials | Unchecked | Login happens. User name is not remembered for next time use. <Is there any need to clear earlier remembered user name?> |
| 5 | User enters invalid credentials | Checked | Login fails. <Display error message - To Be Reviewed>. User name is not remembered for next time use. (Existing remembered user name remains intact) |
| 6 | User enters invalid credentials | Unchecked | Login fails. <Displays error message>. User name is not remembered for next time use. (Existing remembered user name remains intact) |

## Prepare test data

| Sr. No. | User Name | Password |
| --- | --- | --- |
| 1 | very long user name | very long password |
| 2 | Test@#$% | P@$$w0rd w!th spec!al ch@r$ |
| 3 | Test$%^ | P@$$w0rd |
| 4 | T |   |
| 5 | T | T |
| 6 |   |   |
| 7 | UPPERCASE | UPPERCASE |
| 8 | lowercase | lowercase |
| 9 | User |         |
| 10 | MyDomain\\User |     p@ssw0rd with sp@ces    |
| 11 | test.MyDomain\\User2 |   |
| 12 | User@MyDomain |   |
| 13 | User2@test.MyDomain |   |

## List down external factors affecting Test Environment

 Below are some external factors that can affect test execution. And these might not have considered during backlog grooming and hence not listed in Acceptance criteria.

1. User password Expired
2. Domain controller not reachable
3. Account Disabled
4. User has blank password
5. User name has special characters
6. User name is in Unicode (Example: वैभव)

## List Of Identified Use Cases to be considered for each supported OS

| Sr. No. | Use Case | Remember user name | External conditions? | Expected behavior |
| --- | --- | --- | --- | --- |
| 1 | User cancels login | Checked |   | Dialog closes. <Save entered user name? Is this really a requirement? - Is this documented?> |
| 2 | User cancels login | Unchecked |   | Dialog closes. |
| 3 | User enters valid credentials | Checked |   | Login happens. User name is remembered for next time use. |
| 4 | User Launches login dialog | Checked |   | During launch login dialog shows  earlier remembered user name |
| 5 | User enters valid credentials | Unchecked |   | Login happens. User name is not remembered for next time use. <Is there any need to clear earlier remembered user name?> |
| 6 | User Launches login dialog | Unchecked |   | During launch login dialog does not show earlier remembered user name. |
| 7 | User enters valid credentials | Any | User password Expired | <Have we defined expected behavior?> |
| 8 | User enters valid credentials | Any | Domain controller not reachable | <Have we defined expected behavior?> |
| 9 | User enters valid credentials | Any | Account Disabled | <Have we defined expected behavior?> |
| 10 | User enters valid credentials | Any | User has blank password | <Have we defined expected behavior?> |
| 11 | User enters valid credentials | Any | User needs to change password at next logon | <Have we defined expected behavior?> |
| 12 | User Launches login dialog | Checked | New version of software installed | <Have we defined expected behavior?> |
| 13 | User Launches login dialog | Checked | Old version of software installed | <Have we defined expected behavior?> |
| 14 | User Launches login dialog | Checked | New version of software installed that has schema changes the way data is persisted | Migrate old data? <Have we defined expected behavior?> |
| 15 | User enters invalid credentials | Checked |   | Login fails. <Displays error message>. User name is not remembered for next time use. (Existing remembered user name remains intact) |
| 16 | User enters invalid credentials | Unchecked |   | Login fails. <Displays error message>. User name is not remembered for next time use. (Existing remembered user name remains intact) |

The next step is to eliminate some of the use cases that might not have high business value.

 

# Further Reading And References

- [The purpose of unit testing](https://simpleprogrammer.com/the-purpose-of-unit-testing/)
- [What software developers should know about testing and QA](https://dzone.com/articles/what-software-developers-should-know-about-testing)
- [Software testing tips](https://stackify.com/software-testing-tips/)
- The Internet

Let me end this post with the following quote

> We are what we repeatedly do. Excellence, then, is not an act, but a habit. - Aristotle
