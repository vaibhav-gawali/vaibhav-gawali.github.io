---
title: "Estimation challenges, gotcha’s and expectations from developer"
date: 2017-08-15
tags: 
  - "challenges"
  - "estimation"
redirect_from:
  - "/estimation-challenges-gotchas-and-expectations-from-developer/"
  - "/estimation-challenges-gotchas-and-expectations-from-developer"
---

## [What is an estimate](https://en.wikipedia.org/wiki/Estimation)? (From Wikipedia)

> Estimation (or estimating) is the process of finding an estimate, or approximation, which is a value that is usable for some purpose even if input data may be incomplete, uncertain, or unstable.

## [Estimate in software development terms](https://en.wikipedia.org/wiki/Software_development_effort_estimation) (From Wikipedia)

> Software development effort estimation is the process of predicting the most realistic amount of effort (expressed in terms of person-hours or money) required to develop or maintain software based on incomplete, uncertain and noisy input.

In essence, estimation is the essential crux of software development, which is required for following purposes –

1. Evaluation of the total cost of the project
2. Decide on number of engineers (developers, testers and/or business analysts) required on the project
3. Decide tentative release date of the product
4. Decide tentative release date to deliver a feature (or set of features) into existing product

### Estimates can be broadly categorized like below and [other variants also exists](https://en.wikipedia.org/wiki/Software_development_effort_estimation#Estimation_approaches) –

1. Estimate based on Work breakdown structure
2. Guestimate
3. [Predictions and projections](https://www.stevefenton.co.uk/2014/06/beyond-estimates/)
4. Estimate based on past history of the project and team strength

![Estimation: Probability vs Actual Time](/assets/images/estimation-challenges-gotchas-and-expectations-from-developer/AAEAAQAAAAAAAAzrAAAAJDg3Y2Q0MGYzLTZlYWQtNDgyNC1iMDE4LTI3MjRiNzZkM2VmYw.png)

## My experience and observations

When I am asked to give estimate on behalf of team, I feel that it is injustice to the team, why?

Here are some facts –

- On one particular task, time taken by one year experience developer is different than that of 8 year experienced developer. Even same is true for two equally experienced developers
- A new developer when joins existing project he must get familiar with the codebase first to get productive
- I can’t control dependencies on other teams or their delivery schedule
- Initially there is lack of clarity on requirements front
- When project is going on from years and uses legacy and unsupported products, it is a challenge to estimate and find a developer to work on
- Generally it is difficult to break down tasks at the minute level at the start of the project
- I don’t know the technology that may be used in the project (I may know, however what if my team has not yet formed or team members have only specific skill set that is useless for the project)

Going further let’s stick to backlog level estimates, as [project level estimates deserves its own discussion](https://martinfowler.com/tags/estimation.html). 

Estimates based on WBS, even though may not be accurate, they at least identify dependencies, tasks etc. which help in further planning.

## When someone gives his/her own estimates

- They never match, task is either vastly under estimated or overestimated
- Not much efforts are put-in for task breakdown
- Unit testing efforts are generally ignored
- Documentation is not considered as an integral part of estimates
- Testing (by QA) efforts are not considered by developers
- Code review and review comments implementation finds no place while estimating

I have seen that an 8 hour estimated task being worked upon across several sprints and still not being complete. I agree that estimates can’t be accurate, however things like this can cause much damage to delivery schedule. There is either utter ignorance in terms of work breakdown or incompetence/lack of skills/vague user story; whatever the reason may be, this is not at all justifiable when there are strict deadlines to adhere too.

Bottom line is – despite being moved to agile methodology, there is still need of estimation to decide scope, size and budget of the project.

Estimates are needed by everyone – Product Owner, Management, Customer etc. for above mentioned purposes.

## Below are [main challenges in the path of estimation](https://simpleprogrammer.com/2014/10/20/4-biggest-reasons-software-developers-suck-estimation/)

[Unknown unknowns](https://www.youtube.com/watch?v=GiPe1OiKQuk) (term coined by Donald Rumsfeld) – I don’t know what I need to know. These needs to be explored and mitigated.

Known unknowns – I know what I need to know however I don’t know the details. Example: I need to write UI in WPF, however I only know WinForms.

Known knowns – Easy to estimate, however still there is scope of lot of deviation.

Procrastination by stakeholders.

Lack of knowledge of the project.

![](/assets/images/estimation-challenges-gotchas-and-expectations-from-developer/AAEAAQAAAAAAAAqzAAAAJDUyNzdlNjBlLTVkNDktNDQ5ZC04ODhkLWFiNGVlNmEyZTNlOQ.png)

## [Agile estimation](https://www.atlassian.com/agile/estimation) to the rescue?

Agile teams have an interesting way of estimation i.e. in terms of [story point estimation](http://info.thoughtworks.com/rs/thoughtworks2/images/twebook-perspectives-estimation_1.pdf), by using methods such as [planning poker](https://en.wikipedia.org/wiki/Planning_poker), [T-Shirt sizing and many more](http://www.agileadvice.com/2015/10/13/agilemanagement/9-agile-estimation-techniques/). However, with changes in team dynamics, it is difficult to move towards accuracy.

Moreover these are estimates for the team and not for an individual developer/tester. When a backlog needs to be worked upon, one must identify all the tasks that are required for the backlog.

## Underestimation:

My observation is – either generic tasks are added to work on the backlog or only few tasks are added. Sometimes even test cases are also missed and added on the last day. Whatever the reason may be – procrastination/lack of knowledge/utter ignorance; when tasks are not broken down, things generally don’t go as planned and there is task slippage.

## Overestimation:

Sometimes tasks are vastly overestimated, and when they complete, rest of the time is filled with other useless non-productive activities. 

## Expectations from individuals or teams

Great things are not achieved by luck, one needs to work towards achieving the goals to make it happen. I think, an estimation is a step forward towards achieving the goal. 

### Questions to ask yourself

1. Have I included unit testing/test case estimates? (Shouldn’t I write VSTS test cases? Or Coded UI test for my UI?)
2. How many features I am going to cover during implementation of the backlog? Can they be broken down further? Does backlog/user story can be further split (if cannot fit into one sprint)?
3. What am I going to do as documentation for the backlog?
4. Am I absolutely sure about done criteria of the feature?
5. Are there any known unknowns?
6. What about unknown unknowns? How to investigate?
7. Is there any dependency? (If yes, then is it internal or external?)
8. Can I set self-deadline for every task?
9. Is there any need to revise estimates as I make progress?

### Some of the aspects that should be considered during estimation –

1. Localization of the software
2. Security in the software
3. Design / extensibility / API modularity
4. Any unexpected events such as individual PC breakdown, build environment crash etc.
5. Unplanned activities that may pop up in between
6. Skillset of the person who will work on the task

## Conclusion

Estimations are very much important, and we as a software developer are compelled to provide these all the time. So we must take proactive steps to eliminate all the roadblocks (as far as possible) and come up with estimates and then refine estimate as we work on the tasks.

## Further reading:

[5 Ways Software Developers Can Become Better at Estimation](https://simpleprogrammer.com/2014/10/27/5-ways-software-developers-can-become-better-estimation/)

[12 Problems with Software Estimation](http://tuomaspelkonen.com/2010/04/12-problems-with-software-estimation-2/)

[Purpose of Estimation (By Martin Fowler)](https://martinfowler.com/bliki/PurposeOfEstimation.html) – [Complete book is here.](http://info.thoughtworks.com/rs/thoughtworks2/images/twebook-perspectives-estimation_1.pdf)

[The Real Reason We Estimate](https://www.leadingagile.com/2011/09/the-real-reason-we-estimate/)

[What We Do and Don't Know about Software Development Effort Estimation](https://www.infoq.com/articles/software-development-effort-estimation)

[From hour estimates gradually to #NoEstimates](http://blog.karhatsu.com/2013/08/from-hour-estimates-gradually-to.html)

[Beyond Estimates](https://www.stevefenton.co.uk/2014/06/beyond-estimates/)

Happy Coding!!!

**Vaibhav M. Gawali**

Passionate .NET developer, a #10Xer, #productivity maniac, #Agile-list, father & husband who loves to solve difficult problems related to software development.

This article was [originally published on the LinkedIn](https://www.linkedin.com/pulse/estimation-challenges-gotchas-expectations-from-developer-gawali).
