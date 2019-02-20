---
ID: 1730
post_title: 'Showing your log4net logging in your C# application'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/09/17/showing-your-log4net-logging-in-youre-c-application/
published: true
post_date: 2010-09-17 22:38:57
---
<p>If you want to show the log4net logging direct in your application by using a textbox, you can use the following link:</p>  <p><a title="http://weblogs.asp.net/psteele/archive/2010/01/25/live-capture-of-log4net-logging.aspx" href="http://weblogs.asp.net/psteele/archive/2010/01/25/live-capture-of-log4net-logging.aspx">http://weblogs.asp.net/psteele/archive/2010/01/25/live-capture-of-log4net-logging.aspx</a></p>  <p>I tried it and it works great:</p>  <p>&#160;</p>  <pre class="code"><p><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.ComponentModel;
<span style="color: blue">using </span>System.Drawing;
<span style="color: blue">using </span>System.Data;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>System.Windows.Forms;
<span style="color: blue">using </span>log4net.Appender;
<span style="color: blue">using </span>System.Threading;

<span style="color: blue">namespace </span>Rvl.Demo.WindowsFormsApplication.UserControls
{
<span style="color: blue">    public partial class </span><span style="color: #2b91af">SettingsUserControl </span>: <span style="color: #2b91af">UserControl</span>, <span style="color: #2b91af">IAppender
    </span>{</p><pre style="width: 758px; height: 152px" class="code"><span style="color: blue">        private static </span><span style="color: #2b91af">ILog </span>_logger = <span style="color: #2b91af">LogManager</span>.GetLogger(<span style="color: blue">typeof</span>(<span style="color: #2b91af">SettingsUserControl</span>));
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">This logger property is used to log events
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public static </span><span style="color: #2b91af">ILog </span>Logger
        {
            <span style="color: blue">get </span>{ <span style="color: blue">return </span>_logger; }
        }
</pre><a href="http://11011.net/software/vspaste"></a><p>
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Constructor
    </span><span style="color: green">    </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public </span>SettingsUserControl()
        {
            InitializeComponent();
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Show progress in outputTextBox
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;loggingEvent&quot;&gt;&lt;/param&gt;
        </span><span style="color: blue">public void </span>DoAppend(log4net.Core.<span style="color: #2b91af">LoggingEvent </span>loggingEvent) 
        {
            outPutTextBox.AppendText(loggingEvent.MessageObject.ToString() + <span style="color: #2b91af">Environment</span>.NewLine);
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Close the log4net appender
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public void </span>Close()
        {
            <span style="color: green">//throw new NotImplementedException();
        </span>}
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Configure the databases
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;sender&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;e&quot;&gt;&lt;/param&gt;
        </span><span style="color: blue">private void C</span>onfigureDatabasesButton_Click(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
            <span style="color: blue">try
            </span>{
                Cursor = <span style="color: #2b91af">Cursors</span>.WaitCursor;

                outPutTextBox.Clear();
                outPutTextBox.AppendText(<span style="color: #a31515">&quot;Start configuration of the databases&quot; </span>+ <span style="color: #2b91af">Environment</span>.NewLine);
                Logger.Debug(<span style="color: #a31515">&quot;Sp 1 execute...&quot;</span>);
                <span style="color: #2b91af">Thread</span>.Sleep(2000);
                Logger.Debug(<span style="color: #a31515">&quot;Sp 2 execute...&quot;</span>);
                <span style="color: #2b91af">Thread</span>.Sleep(2000);
                Logger.Debug(<span style="color: #a31515">&quot;Sp 3 execute...&quot;</span>);
                <span style="color: #2b91af">Thread</span>.Sleep(2000);
                Logger.Debug(<span style="color: #a31515">&quot;Sp 4 execute...&quot;</span>);
                <span style="color: #2b91af">Thread</span>.Sleep(2000);
                Logger.Debug(<span style="color: #a31515">&quot;Finished&quot;</span>);
            }
            <span style="color: blue">finally
            </span>{
                Cursor = <span style="color: #2b91af">Cursors</span>.Default;
            }
        }
    }
}</p><p>&#160;</p><p><strong>Result</strong></p><p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/09/clip_image002.jpg"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="clip_image002" border="0" alt="clip_image002" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/09/clip_image002_thumb.jpg" width="704" height="567" /></a></p><p>

</p></pre>
<a href="http://11011.net/software/vspaste"></a>