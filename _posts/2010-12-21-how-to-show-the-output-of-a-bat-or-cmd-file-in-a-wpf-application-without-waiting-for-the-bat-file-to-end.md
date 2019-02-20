---
ID: 1847
post_title: 'How to show the output of a *.bat or *.cmd file in a WPF application, without waiting for the *.bat file to end'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/12/21/how-to-show-the-output-of-a-bat-or-cmd-file-in-a-wpf-application-without-waiting-for-the-bat-file-to-end/
published: true
post_date: 2010-12-21 16:03:23
---
<h3>Notes</h3>  <ul>   <li>     <div align="left">The functions       <br />- process.StandardOutput.ReadToEnd();         <br />- process.StandardOutput.Read();         <br />- process.StandardOutput.ReadLine();         <br />will wait for the process to end and then output the result.</div>   </li>    <li>     <div align="left">If you want to show the output during processing, you should use       <br />- process.OutputDataReceived += new DataReceivedEventHandler(ProcessOuputHandler);         <br />- and process.BeginOutputReadLine();</div>   </li>    <li>     <div align="left">Because the BeginOutputReadLine will spawn a new thread, you can’t access the UI directly. If you want to update a textbox, you should use the control.Dispatcher.Invoke function.</div>   </li>    <li>     <div align="left">With the control.Dispatcher.CheckAccess() you can determine if the functions is called from the UI thread or not.</div>   </li>    <li>     <div align="left">[myWpfWindow] is a WPF window containing a textbox with the name [outputTextBox] and a button with the name [testButton].</div>   </li>    <li>     <div align="left">The function [ShowingOutputOfBatFile] is called from a [testButton] click eventhandler </div>   </li> </ul>  <p>&#160;</p>  <h3>Code</h3>  <p>&#160;</p> <a href="http://11011.net/software/vspaste"></a>  <pre class="code"><span style="color: blue">public void </span>ShowingOutputOfBatFile()
{

    <span style="color: #2b91af">ProcessStartInfo </span>startInfo = <span style="color: blue">new </span><span style="color: #2b91af">ProcessStartInfo</span>();
    startInfo.FileName = <span style="color: #a31515">@&quot;C:\Temp\Test.bat&quot;</span>;
    startInfo.Arguments = <span style="color: #a31515">&quot;firstParameter secondParamter&quot;</span>;
    startInfo.RedirectStandardError = <span style="color: blue">true</span>;
    startInfo.RedirectStandardOutput = <span style="color: blue">true</span>;
    startInfo.UseShellExecute = <span style="color: blue">false</span>;
    startInfo.WorkingDirectory = <span style="color: #a31515">@&quot;C:\Temp&quot;</span>;
            
    <span style="color: green">// Use startInfo.CreateNoWindow = HideWindow; if you want to hide the window

    </span><span style="color: blue">using </span>(<span style="color: #2b91af">Process </span>process = <span style="color: blue">new </span><span style="color: #2b91af">Process</span>())
    {
        process.StartInfo = startInfo;
        process.OutputDataReceived += <span style="color: blue">new </span><span style="color: #2b91af">DataReceivedEventHandler</span>(ProcessOuputHandler);
        process.Start();
        process.BeginOutputReadLine();
        <span style="color: blue">while </span>(!process.HasExited)
        {
            <span style="color: green">// Refresh you're WPF window here
            </span>myWpfWindow.Dispatcher.Invoke(<span style="color: #2b91af">DispatcherPriority</span>.Render, EmptyDelegate);
            <span style="color: #2b91af">Thread</span>.Sleep(1000);
        }
    }
}

<span style="color: blue">public void </span>ProcessOuputHandler(<span style="color: blue">object </span>sendingProcess, <span style="color: #2b91af">DataReceivedEventArgs </span>outLine)
{
    <span style="color: blue">if </span>(!<span style="color: #2b91af">String</span>.IsNullOrEmpty(outLine.Data))
    {
        <span style="color: blue">if </span>(!outputTextBox.Dispatcher.CheckAccess())
        {
            <span style="color: green">// Called from a none ui thread, so use dispatcher
            </span><span style="color: #2b91af">ShowLoggingDelegate </span>showLoggingDelegate = <span style="color: blue">new </span><span style="color: #2b91af">ShowLoggingDelegate</span>(ShowLogging);
            outputTextBox.Dispatcher.Invoke(<span style="color: #2b91af">DispatcherPriority</span>.Normal, showLoggingDelegate, outLine.Data);
        }
        <span style="color: blue">else
        </span>{
            <span style="color: green">// Called from UI trhead so just update the textbox
            </span>ShowLogging(outLine.Data);
        };
    }
}

<span style="color: blue">private delegate void </span><span style="color: #2b91af">ShowLoggingDelegate</span>(<span style="color: blue">string </span>text);
<span style="color: blue">private static </span><span style="color: #2b91af">Action </span>EmptyDelegate = <span style="color: blue">delegate</span>() { };

<span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">Show the logging on screen
</span><span style="color: gray">/// &lt;/summary&gt;
/// &lt;param name=&quot;text&quot;&gt;&lt;/param&gt;
</span><span style="color: blue">private void </span>ShowLogging(<span style="color: blue">string </span>text)
{
    myWpfWindow.outputTextBox.AppendText(text);
    myWpfWindow.outputTextBox.ScrollToEnd();
}</pre>
<a href="http://11011.net/software/vspaste"></a>