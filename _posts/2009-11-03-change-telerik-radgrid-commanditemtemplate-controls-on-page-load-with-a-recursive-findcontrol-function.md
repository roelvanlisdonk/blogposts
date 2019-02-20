---
ID: 793
post_title: >
  Change Telerik RadGrid
  CommandItemTemplate controls on page
  load with a recursive FindControl
  function
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/11/03/change-telerik-radgrid-commanditemtemplate-controls-on-page-load-with-a-recursive-findcontrol-function/
published: true
post_date: 2009-11-03 16:22:45
---
<p>If you want to change the controls in the CommandItemTemplate of a Telerik RadGrid, you will have to use a recursive FindControl function, because ASP .NET 2.0 does not ship with a FindControl function that can search for controls in child controls.   <br />    <br /></p>  <pre class="code"><span style="color: blue">     public static class </span><span style="color: #2b91af">ControlFinder
    </span>{
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Recursively finds a control in the controls collection.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;control&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;id&quot;&gt;&lt;/param&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color: blue">public static </span><span style="color: #2b91af">Control </span>FindControlRecursive(<span style="color: #2b91af">Control </span>control, <span style="color: blue">string </span>id)
        {
            <span style="color: green">// Return null if parameter control is null
            </span><span style="color: blue">if </span>(control == <span style="color: blue">null</span>) <span style="color: blue">return null</span>;

            <span style="color: green">// Try to find the control at the current level
            </span><span style="color: #2b91af">Control </span>ctrl = control.FindControl(id);
            <span style="color: blue">if </span>(ctrl == <span style="color: blue">null</span>)
            {
                <span style="color: green">// Loop through child controls
                </span><span style="color: blue">foreach </span>(<span style="color: #2b91af">Control </span>child <span style="color: blue">in </span>control.Controls)
                {
                    <span style="color: green">// Try to find the control at the next level
                    </span>ctrl = FindControlRecursive(child, id);

                    <span style="color: green">// Stop search when control is found
                    </span><span style="color: blue">if </span>(ctrl != <span style="color: blue">null</span>) <span style="color: blue">break</span>;
                }
            }
            <span style="color: blue">return </span>ctrl;        }
    }</pre>
<a href="http://11011.net/software/vspaste"></a>

<br />In the page load:

<br />

<br />

<pre class="code"><span style="color: #2b91af">LinkButton </span>showReports = <span style="color: #2b91af">ControlFinder</span>.FindControlRecursive(<span style="color: blue">this</span>.RadGrid.MasterTableView, <span style="color: #a31515">&quot;showReports&quot;</span>) <span style="color: blue">as </span><span style="color: #2b91af">LinkButton</span>;</pre>

<pre class="code">showReports.Attributes[<span style="color: #a31515">&quot;href&quot;</span>] = @<span style="color: #a31515">&quot;\\MyShare&quot;</span>;</pre>
<a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>