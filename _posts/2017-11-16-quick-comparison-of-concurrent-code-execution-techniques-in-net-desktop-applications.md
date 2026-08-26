---
title: "Quick comparison of concurrent code execution techniques in .NET desktop applications"
date: 2017-11-16
categories: 
  - "dotnet"
tags: 
  - "net"
  - "concurrent"
  - "dotnet"
  - "parallel"
---

In .NET desktop applications there are many ways to execute code concurrently (or in parallel) on a different thread. And there are times when a [skilled C# .NET developer](https://vaibhavgawali.net/excellent-csharp-dotnet-developer-skills/) needs to write code that will execute in parallel for some reason. In this post I have tried to compile possible ways that I could find to achieve concurrent code execution in .NET desktop applications.

This should help you to choose the right way of [concurrent (or parallel) code execution](https://softwareengineering.stackexchange.com/questions/190719/the-difference-between-concurrent-and-parallel-execution?newreg=9dd3b7e692044b1fb0ca615f5ed3f106) in your code.

## Quick comparison of classes that facilitates concurrent code execution in .NET desktop applications

| **Sr. No.** | **Class name (including namespace)** | **WinForm UI Sync options** | **WPF UI Sync options** | **Unhandled Exception Behavior** | **Operation Cancellation option** |
| --- | --- | --- | --- | --- | --- |
| 1 | [System.Threading.Thread](https://docs.microsoft.com/en-in/dotnet/api/system.threading.thread?view=netframework-4.7.1) | [Using Control.Invoke method](https://docs.microsoft.com/en-in/dotnet/api/system.windows.forms.control.invoke?view=netframework-4.7.1#System_Windows_Forms_Control_Invoke_System_Delegate_System_Object___) | [Dispatcher.Invoke](https://docs.microsoft.com/en-in/dotnet/api/system.windows.threading.dispatcher.invoke?view=netframework-4.7.1#System_Windows_Threading_Dispatcher_Invoke_System_Delegate_System_Windows_Threading_DispatcherPriority_System_Object___) | Application crash | Explicit code needs to be written |
| 2 | [System.Threading.ThreadPool](https://docs.microsoft.com/en-in/dotnet/api/system.threading.threadpool?view=netframework-4.7.1) | [Using Control.Invoke method](https://docs.microsoft.com/en-in/dotnet/api/system.windows.forms.control.invoke?view=netframework-4.7.1#System_Windows_Forms_Control_Invoke_System_Delegate_System_Object___) | [Dispatcher.Invoke](https://docs.microsoft.com/en-in/dotnet/api/system.windows.threading.dispatcher.invoke?view=netframework-4.7.1#System_Windows_Threading_Dispatcher_Invoke_System_Delegate_System_Windows_Threading_DispatcherPriority_System_Object___) | Application crash | Explicit code needs to be written |
| 3 | [System.ComponentModel.BackgroundWorker](https://docs.microsoft.com/en-in/dotnet/api/system.componentmodel.backgroundworker?view=netframework-4.7.1) | ProgressChanged and RunWorkerCompleted events. | ProgressChanged and RunWorkerCompleted events. | Any exceptions raised in DoWork event handler can be obtained in RunWorkerCompleted event. | Using CancelAsync method and implementation around checking cancellation request. |
| 4 | [System.Threading.Tasks.Task](https://docs.microsoft.com/en-in/dotnet/api/system.threading.tasks.task?view=netframework-4.7.1) | [TaskScheduler.FromCurrentSynchronizationContext()](https://docs.microsoft.com/en-in/dotnet/api/system.threading.tasks.taskscheduler.fromcurrentsynchronizationcontext?view=netframework-4.7.1#System_Threading_Tasks_TaskScheduler_FromCurrentSynchronizationContext) | [TaskScheduler.FromCurrentSynchronizationContext()](https://docs.microsoft.com/en-in/dotnet/api/system.threading.tasks.taskscheduler.fromcurrentsynchronizationcontext?view=netframework-4.7.1#System_Threading_Tasks_TaskScheduler_FromCurrentSynchronizationContext) | Exceptions are reported only when tasks are awaited or result is obtained from task. | Using CancellationToken. Task exeuction code needs to use CancellationToken to cancel running operation and implementation around checking cancellation request. |
| 5 | [System.Threading.Timer](https://docs.microsoft.com/en-in/dotnet/api/system.threading.timer?view=netframework-4.7.1) | [Using Control.Invoke method Or using Control.BeginInvoke method](https://docs.microsoft.com/en-in/dotnet/api/system.windows.forms.control.invoke?view=netframework-4.7.1#System_Windows_Forms_Control_Invoke_System_Delegate_System_Object___) | Using [Dispatcher.Invoke](https://docs.microsoft.com/en-in/dotnet/api/system.windows.threading.dispatcher.invoke?view=netframework-4.7.1#System_Windows_Threading_Dispatcher_Invoke_System_Action_System_Windows_Threading_DispatcherPriority_) method Or using Dispatcher.BeginInvoke method | Application crash | Explicit code needs to be written |
| 6 | [System.Timers.Timer](https://docs.microsoft.com/en-in/dotnet/api/system.timers.timer?view=netframework-4.7.1) | [Using Timer.SynchronizingObject](https://docs.microsoft.com/en-in/dotnet/api/system.timers.timer.synchronizingobject?view=netframework-4.7.1) | Possible by implementing [ISynchronizeInvoke interface](https://docs.microsoft.com/en-in/dotnet/api/system.componentmodel.isynchronizeinvoke?view=netframework-4.7.1). | No crash observed. | Explicit code needs to be written |
| 7 | [System.Windows.Forms.Timer](https://docs.microsoft.com/en-in/dotnet/api/system.windows.forms.timer?view=netframework-4.7.1) | N/A Single threaded; runs on UI thread only. | N/A | Application crash | N/A |
| 8 | [System.Windows.Threading.DispatcherTimer](https://docs.microsoft.com/en-in/dotnet/api/system.windows.threading.dispatchertimer?view=netframework-4.7.1) | N/A | N/A Single threaded; runs on UI thread only. | Application crash | N/A |

 

![Concurrent code execution techniques in .NET desktop applications](/assets/images/quick-comparison-of-concurrent-code-execution-techniques-in-net-desktop-applications/Concurrent-code-execution-techniques.png)
