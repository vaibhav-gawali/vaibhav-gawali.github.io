---
title: "Exception filters in C# 6.0"
date: 2017-08-14
categories: 
  - "csharp"
tags: 
  - "csharp"
  - "dotnet"
---

Learn how to use exception filtering technique introduced in C# 6.0.

This video has been published on YouTube.

* * *

\[embed\]https://youtu.be/5yBRnKrxggI\[/embed\]

* * *

### Code Samples

<!--more-->

```
namespace ExceptionFilters
{
    class Program
    {
        static int Main(string[] args)
        {
            #region Old way of filtering exceptions
            int recoveryMode;
            try
            {
                DoOperation(null);
                //DoOperation(1,2,3,4);
            }
            catch (ArgumentOutOfRangeException ae)
            {
                LogException(ae);
                if (CanRecover(ae)) { Recover(ae); }
                else if (CanRecover(ae, out recoveryMode)) { Recover(ae, recoveryMode); }
                else if (ae.Message.Contains("warning")) { Recover(ae); }
                else { throw; }
            }
            catch (Exception e)
            {
                LogException(e);
                if (CanRecover(e)) { Recover(e); }
                else if (CanRecover(e, out recoveryMode)) { Recover(e, recoveryMode); }
                else if (e.Message.Contains("warning")) { Recover(e); }
                else { throw; }
            }

            #endregion Old way of filtering exceptions
            
            #region Exception Filters
            //return 0;
            try
            {
                DoOperation(null);
                //DoOperation(1,2,3,4);
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
            catch( Exception e) when (e.Message.Contains("warning"))
            {
                Recover(e);
            }
            catch(ArgumentNullException ane)
            {
                //Handle argument null exception
            }

            #endregion Exception Filters

            return 0; //Success
        }

        #region Helper Methods
        private static void Recover(Exception e, int recoveryMode)
        {
            Console.ForegroundColor = ConsoleColor.DarkGreen;
            Console.WriteLine($"Recovered {e.Message} Recovery mode: {recoveryMode}");
            Console.ResetColor();
        }

        static void Recover(Exception e)
        {
            Recover(e, 2);
        }

        static void DoOperation(params object[] arguments)
        {
            if (arguments == null) { throw new ArgumentException($"{nameof(arguments)} cannot be null."); }

            if (arguments.Length > 3)
            {
                throw new ArgumentOutOfRangeException(nameof(arguments), $"{nameof(arguments)} is out of range. Upto 3 arguments are allowed.");
            }
        }

        static bool CanRecover(Exception ex)
        {
            ArgumentOutOfRangeException aoore = ex as ArgumentOutOfRangeException;
            return aoore != null;
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
            return false;
        }

        #endregion Helper Methods
    }
}
```
