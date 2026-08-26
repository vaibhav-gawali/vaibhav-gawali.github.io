---
title: "Tips on raising event to all event listeners even if listeners raise an exception"
date: 2018-04-04
categories: 
  - "dotnet"
  - "csharp"
tags: 
  - "net"
  - "csharp"
  - "delegates"
  - "dotnet"
  - "events"
redirect_from:
  - "/tips-on-raising-event-to-all-event-listeners-even-if-listeners-raise-an-exception/"
  - "/tips-on-raising-event-to-all-event-listeners-even-if-listeners-raise-an-exception"
---

By default with default event raising mechanism of C# generated code, CLR aborts raising events to other subscribers when an exception is raised by one of the subscriber. And sometimes it is necessary to raise event to all event listeners even when some of the event subscribers fails by raising an exception.

I myself has faced this situation some of the times and below code can help to address this. Off-course, you should also have a error reporting mechanism built-into your class, otherwise you will end up swallowing all of the exceptions.

Note that below code snippet only focuses on raising events to all of the subscribers, despite failures in some of the event subscribers. And does not account for [threading](https://vaibhavgawali.net/quick-comparison-of-concurrent-code-execution-techniques-in-net-desktop-applications/) and follow best practices like [Exception handling](https://vaibhavgawali.net/csharp-dotnet-exception-handling-best-practices/) etc. and these are [important considerations in real world applications](https://vaibhavgawali.net/observations-from-code-reviews-and-why-they-are-important/). As a [skilled professional C# .NET developer](https://vaibhavgawali.net/excellent-csharp-dotnet-developer-skills/) you should consider implementing best practices in your code along with [good quality test cases](https://vaibhavgawali.net/are-you-doing-effective-testing/).

![Use of invocation list to notify each event subscriber individually](/assets/images/tips-on-raising-event-to-all-event-listeners-even-if-listeners-raise-an-exception/Use-of-invocation-list-to-notify-each-event-subscriber-individually.png)

Here is the code snippet ([Try running this code on .NET Fiddle](https://dotnetfiddle.net/rNR7m6)):

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace EffectiveDeveloper.Events.Demo
{
    class Program
    {
        static void Main(string[] args)
        {
            Publisher publisher = new Publisher();
            BadSubscriber subscriber1 = new BadSubscriber(publisher);
            GoodSubscriber subscriber2 = new GoodSubscriber(publisher);

            publisher.Publish();
        }
    }

    class Publisher
    {
        public event EventHandler Notify;
        

        public void Publish()
        {
            Console.WriteLine("Publishing data...");
            //Publish your stuff here and then it is time to notify.
            EventHandler eh = Notify;
            if(eh == null)
            {
                return;
            }
            List<Exception> errors = null;
            Delegate[] subscribers = eh.GetInvocationList();
            foreach(EventHandler subscriber in subscribers)
            {
                try { subscriber(this, EventArgs.Empty); }
                catch (Exception ex)
                {
                    if(errors == null) { errors = new List<Exception>(1); }
                    errors.Add(ex);
                }
            }
            if (errors != null)
            {
                ReportErrors(errors);
            }
            Console.WriteLine("Publishing data complete.");
        }

        void ReportErrors(List<Exception> errors)
        {
            //Logic goes here
            Console.WriteLine("Some of the subscribers failed to process requests. Failed subscriber count {0}.", errors.Count);
            foreach (Exception error in errors)
            {
                Console.WriteLine(error);
            }
        }
    }

    class GoodSubscriber
    {
        Publisher _publisher;
        public GoodSubscriber(Publisher publisher)
        {
            _publisher = publisher;
            _publisher.Notify += _publisher_Notify;
        }

        private void _publisher_Notify(object sender, EventArgs e)
        {
            Console.WriteLine("Publishers event is processed.");
        }
    }
    class BadSubscriber
    {
        Publisher _publisher;
        public BadSubscriber(Publisher publisher)
        {
            _publisher = publisher;
            _publisher.Notify += _publisher_Notify;
        }

        private void _publisher_Notify(object sender, EventArgs e)
        {
            Console.WriteLine("Error: Cannot process publish request.");
            throw new InvalidOperationException("Cannot process publish request.");
        }
    }
}
```
