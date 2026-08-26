---
title: "Exception handling best practices"
date: 2017-09-17
categories: 
  - "dotnet"
  - "csharp"
tags: 
  - "net"
  - "csharp"
  - "dotnet"
  - "exception"
---

Excellent exception handling is must for any app for excellent user experience and it is an essential trait of an [excellent C# developer](https://vaibhavgawali.net/excellent-csharp-dotnet-developer-skills/).

# Tips for Exception handling best practices

## Always validate public method parameters and raise appropriate exceptions

If you accept any erroneous input in the method argument, and when external clients use the API, then later on it becomes very expensive to fix the issue.

Never ever allow erroneous argument in the public method of class. Validate extensively and raise ArguementException or ArgumentNullException as appropriate. [See below code sample.](#CodeSample)

## Design class/interface such that there is no need to raise an Exception for common scenarios

Raising an exception is a costly operation under the hood. And when class API is designed such that it guarantees not to raise an exception, this improves application performance tremendously, if API is frequently used.

Example: Refer int.TryParse pattern. [Also refer below sample code](#CodeSample).

\[caption id="attachment\_443" align="aligncenter" width="1267"\]![Exception Handling Best Practices](/assets/images/csharp-dotnet-exception-handling-best-practices/ExceptionHandlingBestPractices.png) Exception Handling Best Practices\[/caption\]

## Types of Exceptions to be raised from your code

Below types of Exceptions you should raise from your code -

ArgumentException, ArgumentNullException, ArgumentOutOfRangeException, InvalidOperationException.

.NET framework reserved exceptions such as NullRefenceException, OutOfMemoryException, IndexOutOfRangeException should not be raised.

Do not raise generic Exception (sadly Microsoft's own code samples follow this practice).

Consider creating custom exception as a last option. And when a custom exception is defined it must be marked with Serializable attribute so that they can cross AppDomain and COM boundaries.

## Maintain stack trace

Stack trace of exception must be maintained unless there is strong reason to erase stack trace.

[Use exception filters](https://vaibhavgawali.net/exception-filters-in-c-6-0/) as far as possible to log exceptions and preserve stack trace.

Use “throw;” statement instead of “throw ex;”, later erases the stack trace.

## Dispose of resources you no longer need

Once you are done with the disposable objects or COM objects or native un-managed resources just dispose them off in the finally block. [Refer my other post that mentions about memory leaks in .NET](https://vaibhavgawali.net/observations-from-code-reviews-and-why-they-are-important/#MemoryLeaks).

## Avoid suppressing exception without taking any action

When you suppress exception, it becomes very difficult to find and resolve issues. Consider logging exception to log file (or to some centralized place such as database or windows event log).

Log files can be used for issues debugging and fixing app crash type of scenarios. Log the full stack trace and not just error message.

Also when user is interacting with UI (example clicking OK button) and there is no response (because application suppresses an exception), it results into frustration. Hence you should notify user about errors encountered.

Usually a well tested UI will never display errors to user unless there is some issue, such as database is down.

## Have a localization strategy for exception messages

There may not be any need to localize every single exception message in your application. However the error messages that are targeted for end user, must be localized.

## In your executable always subscribe to AppDomain's UnhandledException event.

This ensures that you log an exception into log file or somewhere useful location for later post-martam debugging.

## Subscribe to FirstChanceException

Subscribe to FirstChanceException to know problematic areas of your application that might be causing performance degradation.

It is also possible that any 3rd party libraries used might be degrading application performance by raising lot of First Chance Exceptions. This is the way to find out.

Ensure that you refactor your code not to raise First Chance Exception unless absolutely necessary.

## Subscribe to WPF Dispature's unhandled exception events

This helps to notify user about any uncaught exceptions, and also gives you a chance to recover from them. See the code sample below for reference.

## Code Sample

```
namespace BestPractices.ExceptionHandling
{
    class Operation : IDisposable
    {
        static TraceSwitch s_traceSwitch = new TraceSwitch("Operation", "Operation", "On");

        MemoryStream _memoryStream;

        public Operation()
        {
            _memoryStream = new MemoryStream();
        }

        public bool TryDoOperation(params string[] arguments)
        {
            if (s_traceSwitch.TraceVerbose)
            {
                Trace.WriteLine(((FormattableString)$"Entry: {nameof(Operation)}.{nameof(TryDoOperation)}").ToString(CultureInfo.InvariantCulture));
            }
            ValidateDisposedState();
            if(arguments == null || arguments.Length < 1 || arguments.Length > 3)

            {

                if (s_traceSwitch.TraceWarning)
                {
                    Trace.WriteLine(((FormattableString)$"{nameof(Operation)}.{nameof(TryDoOperation)}: Skipped because of invalid arguments.").ToString(CultureInfo.InvariantCulture));
                }
                return false;
            }
            WriteToMemoryStream(arguments);
            if (s_traceSwitch.TraceVerbose)
            {
                Trace.WriteLine(((FormattableString)$"Exit: {nameof(Operation)}.{nameof(TryDoOperation)}").ToString(CultureInfo.InvariantCulture));
            }
            return true;
        }

        public void DoOperation(params string[] arguments)
        {
            if (s_traceSwitch.TraceVerbose)
            {
                Trace.WriteLine(((FormattableString)$"Entry: {nameof(Operation)}.{nameof(DoOperation)}").ToString(CultureInfo.InvariantCulture));
            }
            ValidateDisposedState();
            ValidateArguments(arguments);

            WriteToMemoryStream(arguments);

            if (s_traceSwitch.TraceVerbose)
            {
                Trace.WriteLine(((FormattableString)$"Exit: {nameof(Operation)}.{nameof(DoOperation)}").ToString(CultureInfo.InvariantCulture));
            }
        }

        private void WriteToMemoryStream(string[] arguments)
        {
            //Logic goes here
        }

        private static void ValidateArguments(string[] arguments)
        {
            if (arguments == null)
            {
                if (s_traceSwitch.TraceError)
                {
                    Trace.WriteLine(((FormattableString)$"{nameof(Operation)}.{nameof(ValidateArguments)}: Error - arguments null.").ToString(CultureInfo.InvariantCulture));
                }
                throw new ArgumentException($"{nameof(arguments)} cannot be null.");
            }
            
            if (arguments.Length < 1)
            {
                if (s_traceSwitch.TraceError)
                {
                    Trace.WriteLine(((FormattableString)$"{nameof(Operation)}.{nameof(ValidateArguments)}: Error - zero length string argument array.").ToString(CultureInfo.InvariantCulture));
                }
                throw new ArgumentException($"{nameof(arguments)} cannot be zero length.");
            }

            if (arguments.Length > 3)
            {
                if (s_traceSwitch.TraceError)
                {
                    Trace.WriteLine(((FormattableString)$"{nameof(Operation)}.{nameof(ValidateArguments)}: Error - String argument array length must not be greater than three.").ToString(CultureInfo.InvariantCulture));
                }
                throw new ArgumentOutOfRangeException(nameof(arguments), $"{nameof(arguments)} is out of range. Upto 3 arguments are allowed.");
            }
        }

        private void ValidateDisposedState()
        {
            if(_memoryStream == null)
            {
                if (s_traceSwitch.TraceError)
                {
                    Trace.WriteLine(((FormattableString)$"{nameof(Operation)}.{nameof(ValidateDisposedState)}: Error - Operation is disposed.").ToString(CultureInfo.InvariantCulture));
                }
                throw new ObjectDisposedException(nameof(Operation));
            }
        }

        public void Dispose()
        {
            if (s_traceSwitch.TraceVerbose)
            {
                Trace.WriteLine(((FormattableString)$"Entry: {nameof(Operation)}.{nameof(Dispose)}").ToString(CultureInfo.InvariantCulture));
            }

            if (_memoryStream != null)
            {
                if (s_traceSwitch.TraceInfo)
                {
                    Trace.WriteLine(((FormattableString)$"{nameof(Operation)}.{nameof(Dispose)}: Disposing memory stream").ToString(CultureInfo.InvariantCulture));
                }
                _memoryStream.Dispose();
                _memoryStream = null;
            }

            if (s_traceSwitch.TraceVerbose)
            {
                Trace.WriteLine(((FormattableString)$"Exit: {nameof(Operation)}.{nameof(Dispose)}").ToString(CultureInfo.InvariantCulture));
            }
        }
    }
    class Program
    {
        static TraceSwitch s_traceSwitch = new TraceSwitch("Default", "Default", "On");

        static int Main(string[] args)
        {
            if (s_traceSwitch.TraceVerbose)
            {
                Trace.WriteLine(((FormattableString)$"Entry: {nameof(Program)}.{nameof(Main)}").ToString(CultureInfo.InvariantCulture));
            }
            //In your executable always subscribe to Appdomains UnhandledException event.
            AppDomain.CurrentDomain.UnhandledException += CurrentDomain_UnhandledException;

            //Subscrube to FirstChanceException to know problematic areas of your application that might be causing performance degradation
            //Or perhaps you are using third party libraries and you want to know 
            AppDomain.CurrentDomain.FirstChanceException += CurrentDomain_FirstChanceException;

            //For WinForms App, Application.ThreadException event can be subscribed, but I suggest not to use it as AppDomain.CurrentDomain.UnhandledException will anyway be raised
            System.Windows.Forms.Application.ThreadException += Application_ThreadException;

            //Subscribe below events for WPF application
            System.Windows.Threading.Dispatcher.CurrentDispatcher.UnhandledException += CurrentDispatcher_UnhandledException;
            System.Windows.Threading.Dispatcher.CurrentDispatcher.UnhandledExceptionFilter += CurrentDispatcher_UnhandledExceptionFilter;

            #region Exception Handling
            int recoveryMode;
            Operation op = null;
            try
            {
                op = new Operation();
                op.DoOperation(null);
                //op.DoOperation(1,2,3,4);
            }
            catch (Exception e) when (LogException(e))
            {
                //This block is intentianally left empty, just an exception is logged 
                //in an exception filter
            }
            catch (Exception e) when (CanRecover(e))
            {
                Recover(e);
            }
            catch (Exception e) when (CanRecover(e, out recoveryMode))
            {
                Recover(e, recoveryMode);
            }
            catch (Exception e) when (e.Message.Contains("warning"))
            {
                Recover(e);
            }
            catch (ArgumentNullException ane)
            {
                //Handle argument null exception
            }
            finally
            {
                if(op != null)
                {
                    op.Dispose();
                }
            }

            #endregion Exception Handling

            if (s_traceSwitch.TraceVerbose)
            {
                Trace.WriteLine(((FormattableString)$"Exit: {nameof(Program)}.{nameof(Main)}").ToString(CultureInfo.InvariantCulture));
            }
            return 0;
        }

        #region Unhandled exception handler methods
        private static void Application_ThreadException(object sender, System.Threading.ThreadExceptionEventArgs e)
        {
            
        }

        private static void CurrentDomain_FirstChanceException(object sender, System.Runtime.ExceptionServices.FirstChanceExceptionEventArgs e)
        {
            //Find out how many unwanted exceptions are getting raised and tweak your code to avoid first chance exceptions
        }

        private static void CurrentDispatcher_UnhandledException(object sender, System.Windows.Threading.DispatcherUnhandledExceptionEventArgs e)
        {
            //Log exception and display error message to user 
            e.Handled = true;
        }

        private static void CurrentDispatcher_UnhandledExceptionFilter(object sender, System.Windows.Threading.DispatcherUnhandledExceptionFilterEventArgs e)
        {
            //Log exception
            e.RequestCatch = true;
        }

        private static void CurrentDomain_UnhandledException(object sender, UnhandledExceptionEventArgs e)
        {
            //Log exception and notify user
            if(e.IsTerminating)
            {
                //Oops!!! Your app can't run.
            }            
        }
        #endregion Unhandled exception handler methods

        #region Helper Methods
        static void Recover(Exception e, int recoveryMode)
        {
            Console.ForegroundColor = ConsoleColor.DarkGreen;
            Console.WriteLine($"Recovered {e.Message} Recovery mode: {recoveryMode}");
            Console.ResetColor();
            if (s_traceSwitch.TraceInfo)
            {
                Trace.TraceError(((FormattableString)$"{nameof(Recover)}: Recovered from {e}").ToString(CultureInfo.InvariantCulture));
            }
        }

        static void Recover(Exception e)
        {
            Recover(e, 2);
        }

        static bool CanRecover(Exception ex)
        {
            ArgumentOutOfRangeException aoore = ex as ArgumentOutOfRangeException;

            bool isRecoverable = aoore != null;
            if (false == isRecoverable && s_traceSwitch.TraceError )
            {
                Trace.TraceError(((FormattableString)$"{nameof(CanRecover)}: Cannot recover from {ex}").ToString(CultureInfo.InvariantCulture));
            }
            return isRecoverable;
        }

        static bool CanRecover(Exception ex, out int recoveryMode)
        {
            recoveryMode = 1;
            return false;
        }

        static bool LogException(Exception ex)
        {
            Console.ForegroundColor = ConsoleColor.Red;
            Console.WriteLine($"Exception occured: {ex}");
            Console.ResetColor();
            if (s_traceSwitch.TraceError)
            {
                Trace.TraceError(((FormattableString)$"{nameof(LogException)}: {ex}").ToString(CultureInfo.InvariantCulture));
            }
            return false;
        }

        #endregion Helper Methods
    }
}
```
