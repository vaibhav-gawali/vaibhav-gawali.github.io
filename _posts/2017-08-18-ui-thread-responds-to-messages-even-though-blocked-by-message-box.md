---
title: "UI thread responds to messages even though it is blocked by message box"
date: 2017-08-18
categories: 
  - "dotnet"
tags: 
  - "net"
  - "thread"
  - "ui"
  - "winform"
  - "wpf"
redirect_from:
  - "/ui-thread-responds-to-messages-even-though-blocked-by-message-box/"
  - "/ui-thread-responds-to-messages-even-though-blocked-by-message-box"
---

My observation is that many times developer assume that when a message box is getting displayed then UI thread is just blocked. And UI thread cannot do anything else.

However this is not true, UI thread do respond to low level messages that are being received via mechanisms like timer event, graphics drawing etc.

To demonstrate this to one of my colleague, I came up with following approach for windows form environment

1. In WinForms app added a timer that runs on a separate thread and notifies every two seconds
2. Displayed message box when timer event is received
3. Note that user cannot do anything on the form when message box is being displayed, however Form do respond to message pump messages

This is also true for a WPF application.

```csharp
public partial class MultipleMessageBox : Form
    {
        private System.ComponentModel.IContainer components = null;
        private System.Windows.Forms.Button btnStartTimer;

        System.Timers.Timer _timerMessageDisplay;
        bool _canDisplayMessage;

        public MultipleMessageBox()
        {
            InitializeComponent();
            _timerMessageDisplay = new System.Timers.Timer(2000d); //Show message every two seconds
            _timerMessageDisplay.Elapsed += _timerMessageDisplay_Elapsed;
            _timerMessageDisplay.Enabled = false;
            _timerMessageDisplay.SynchronizingObject = this;
        }
            
        private void _timerMessageDisplay_Elapsed(object sender, System.Timers.ElapsedEventArgs e)
        {
            MessageBox.Show(this, "Test", this.Text, MessageBoxButtons.OK, MessageBoxIcon.Information);
        }

        private void btnStartTimer_Click(object sender, EventArgs e)
        {
            //
            
            _timerMessageDisplay.Enabled = _canDisplayMessage = !_canDisplayMessage;

            btnStartTimer.Text = _canDisplayMessage ? "Stop Displaying Message" : "Start Displaying Message";
            
        }

        private void InitializeComponent()
        {
            this.btnStartTimer = new System.Windows.Forms.Button();
            this.SuspendLayout();
            // 
            // btnStartTimer
            // 
            this.btnStartTimer.Location = new System.Drawing.Point(12, 12);
            this.btnStartTimer.Name = "btnStartTimer";
            this.btnStartTimer.Size = new System.Drawing.Size(153, 23);
            this.btnStartTimer.TabIndex = 0;
            this.btnStartTimer.Text = "Start Displaying Message";
            this.btnStartTimer.UseVisualStyleBackColor = true;
            this.btnStartTimer.Click += new System.EventHandler(this.btnStartTimer_Click);
            // 
            // MultipleMessageBox
            // 
            this.AutoScaleDimensions = new System.Drawing.SizeF(6F, 13F);
            this.AutoScaleMode = System.Windows.Forms.AutoScaleMode.Font;
            this.ClientSize = new System.Drawing.Size(416, 234);
            this.Controls.Add(this.btnStartTimer);
            this.Name = "MultipleMessageBox";
            this.Text = "Multiple Message Box\'s";
            this.ResumeLayout(false);

        }
    }
```

![Multiple message box displayed on same thread](/assets/images/ui-thread-responds-to-messages-even-though-blocked-by-message-box/MultipleMessageBox_display_on_same_thread.png)

So question remains when should we consider that UI thread (or any thread per say) is blocked?

And simple answer is - a thread cannot process any other request till it is executing some form of code and not waiting on something.
