---
ID: 1855
post_title: >
  How to enable logging for Dts.Log
  statements in a SSIS Script Task
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/12/24/how-to-enable-logging-for-dts-log-statements-in-a-ssis-script-task/
published: true
post_date: 2010-12-24 11:19:28
---
<p>If you want to log from a script task, you can use the Dts.Log function. </p>  <p>This function can log to the system table: dbo.sysssislog. If you configure you’re package logging correctly.</p>  <p>&#160;</p>  <p><strong>Notes</strong></p>  <p>Most importantly, if you want to log from a script task by using the function Dts.Log, enable logging for the specific script task and enable &quot;<strong>ScriptTaskLogEntry</strong>&quot;</p>  <p>&#160;</p>  <table border="1" cellspacing="0" cellpadding="2" width="750"><tbody>     <tr>       <td valign="top" width="750"><strong>Steps to enable logging from within you SSIS script task</strong></td>     </tr>      <tr>       <td valign="top" width="750">Make sure you’re Script Task contains a Dts.Log function call, like:         <br />          <pre class="code"><p><span style="color: blue">public void </span>Main()
{
    <span style="color: green">// Define log message
    </span><span style="color: blue">string </span>message = <span style="color: #a31515">&quot;This is my log text&quot;</span>;
                
    <span style="color: green">// Log the message
    </span>Dts.Log(message, 999, <span style="color: blue">null</span>);
    
    Dts.TaskResult = (<span style="color: blue">int</span>)<span style="color: #2b91af">ScriptResults</span>.Success;
}</p></pre>
      </td>
    </tr>

    <tr>
      <td valign="top" width="750">In the control flow right click and choose Logging…
        <br />Check all checkboxes in the treeview, make sure the script task is not grayed out or unchecked

        <br />Click on the top node in the treeview and add SSIS log provider for SQL Server:

        <br />

        <br />&#160;<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/12/image1.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/12/image_thumb1.png" width="695" height="516" /></a> </td>
    </tr>

    <tr>
      <td valign="top" width="750">Enable ScriptTaskLogEntry in the details tab of the script task
        <br />

        <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/12/image2.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/12/image_thumb2.png" width="700" height="520" /></a> 

        <br /></td>
    </tr>

    <tr>
      <td valign="top" width="750">When you run this package, you should see the logging in the table dbo.sysssislog</td>
    </tr>
  </tbody></table>