---
ID: 1184
post_title: 'How to get the current selected MailItem, TaskItem or AppointmentItem in C#, when contextmenu item is clicked in Microsoft Outlook 2010'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/04/07/how-to-get-the-current-selected-mailitem-taskitem-or-appointmentitem-in-c-when-contextmenu-item-is-clicked-in-microsoft-outlook-2010/
published: true
post_date: 2010-04-07 13:02:52
---
<p>If you use a contextmenu in you’re Microsoft Outlook 2010 C# add-in and want to use the item the user clicked on, you should use the first object in the</p>  <pre class="code"><span style="color: #2b91af">Globals</span>.ThisAddIn.Application.ActiveExplorer().Selection</pre>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image_thumb.png" width="804" height="484" /></a> </p>

<p>&#160;</p>

<p><strong>Note</strong></p>

<p>The Selection collection does not start at index 0 but index 1, if you use Selection[0] an index out of bounds exception will occur.</p>

<p>&#160;</p>

<p><strong>ContextMenu.xml</strong></p>

<pre class="code"><span style="color: blue">&lt;?</span><span style="color: #a31515">xml </span><span style="color: red">version</span><span style="color: blue">=</span>&quot;<span style="color: blue">1.0</span>&quot; <span style="color: red">encoding</span><span style="color: blue">=</span>&quot;<span style="color: blue">UTF-8</span>&quot;<span style="color: blue">?&gt;
&lt;</span><span style="color: #a31515">customUI </span><span style="color: red">xmlns</span><span style="color: blue">=</span>&quot;<span style="color: blue">http://schemas.microsoft.com/office/2009/07/customui</span>&quot; <span style="color: red">onLoad</span><span style="color: blue">=</span>&quot;<span style="color: blue">Ribbon_Load</span>&quot;<span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">contextMenus</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">contextMenu </span><span style="color: red">idMso</span><span style="color: blue">=</span>&quot;<span style="color: blue">ContextMenuFolder</span>&quot;<span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">button </span><span style="color: red">idMso</span><span style="color: blue">=</span>&quot;<span style="color: blue">FolderPropertiesContext</span>&quot; <span style="color: red">getVisible</span><span style="color: blue">=</span>&quot;<span style="color: blue">IsVisible</span>&quot; <span style="color: blue">/&gt;
            
        &lt;/</span><span style="color: #a31515">contextMenu</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">contextMenu </span><span style="color: red">idMso</span><span style="color: blue">=</span>&quot;<span style="color: blue">ContextMenuMailItem</span>&quot;<span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">button </span><span style="color: red">id</span><span style="color: blue">=</span>&quot;<span style="color: blue">MyContextMenuMailItem</span>&quot;
            <span style="color: red">label</span><span style="color: blue">=</span>&quot;<span style="color: blue">Start Timer</span>&quot;
            <span style="color: red">onAction</span><span style="color: blue">=</span>&quot;<span style="color: blue">OnMyButtonClick</span>&quot;<span style="color: blue">/&gt;
        &lt;/</span><span style="color: #a31515">contextMenu</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">contextMenu </span><span style="color: red">idMso</span><span style="color: blue">=</span>&quot;<span style="color: blue">ContextMenuTaskItem</span>&quot;<span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">button </span><span style="color: red">id</span><span style="color: blue">=</span>&quot;<span style="color: blue">MyContextMenuTaskItem</span>&quot;
                    <span style="color: red">label</span><span style="color: blue">=</span>&quot;<span style="color: blue">Start Timer</span>&quot;
                    <span style="color: red">onAction</span><span style="color: blue">=</span>&quot;<span style="color: blue">OnMyButtonClick</span>&quot;<span style="color: blue">/&gt;
        &lt;/</span><span style="color: #a31515">contextMenu</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">contextMenu </span><span style="color: red">idMso</span><span style="color: blue">=</span>&quot;<span style="color: blue">ContextMenuCalendarItem</span>&quot;<span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">button </span><span style="color: red">id</span><span style="color: blue">=</span>&quot;<span style="color: blue">MyContextMenuCalendarItem</span>&quot;
          <span style="color: red">label</span><span style="color: blue">=</span>&quot;<span style="color: blue">Start Timer</span>&quot;
          <span style="color: red">onAction</span><span style="color: blue">=</span>&quot;<span style="color: blue">OnMyButtonClick</span>&quot;<span style="color: blue">/&gt;
        &lt;/</span><span style="color: #a31515">contextMenu</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">contextMenus</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">customUI</span><span style="color: blue">&gt;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><strong>ContextMenu.cs</strong></p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.IO;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Reflection;
<span style="color: blue">using </span>System.Runtime.InteropServices;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>Microsoft.Office.Interop.Outlook;
<span style="color: blue">using </span>Office = Microsoft.Office.Core;
<span style="color: blue">using </span>Ada.Tip.WpfUserControls.BC;

<span style="color: blue">namespace </span>Ada.Tip.OutlookAddIn
{
    [<span style="color: #2b91af">ComVisible</span>(<span style="color: blue">true</span>)]
    <span style="color: blue">public class </span><span style="color: #2b91af">ContextMenuRibbon </span>: Office.<span style="color: #2b91af">IRibbonExtensibility
    </span>{
        <span style="color: blue">private </span>Office.<span style="color: #2b91af">IRibbonUI </span>ribbon;

        <span style="color: blue">public </span>ContextMenuRibbon()
        {
        }        
        <span style="color: blue">public bool </span>IsVisible(Office.<span style="color: #2b91af">IRibbonControl </span>control)
        {
            <span style="color: green">//string foldername = ((Microsoft.Office.Interop.Outlook.Folder)control.Context).Name;
            //if (foldername == &quot;Inbox&quot;)
            //{
            //  return false;
            //}
            </span><span style="color: blue">return true</span>;
        }
        <span style="color: blue">#region </span>IRibbonExtensibility Members

        <span style="color: blue">public string </span>GetCustomUI(<span style="color: blue">string </span>ribbonID)
        {
            <span style="color: blue">return </span>GetResourceText(<span style="color: #a31515">&quot;Ada.Tip.OutlookAddIn.contextMenuRibbon.xml&quot;</span>);
        }

        <span style="color: blue">#endregion

        #region </span>Ribbon Callbacks
        <span style="color: green">//Create callback methods here. For more information about adding callback methods, select the Ribbon XML item in Solution Explorer and then press F1
        </span><span style="color: blue">public void </span>Ribbon_Load(Office.<span style="color: #2b91af">IRibbonUI </span>ribbonUI)
        {
            <span style="color: blue">this</span>.ribbon = ribbonUI;
            <span style="color: #2b91af">Globals</span>.ThisAddIn.RibbonUI = ribbonUI;
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Event fires when user clicks in the ContextMenu on &quot;Start Timer&quot;
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;control&quot;&gt;&lt;/param&gt;
        </span><span style="color: blue">public void </span>OnMyButtonClick(Office.<span style="color: #2b91af">IRibbonControl </span>control)
        {
            <span style="color: #2b91af">Globals</span>.ThisAddIn.dashboardUserControl.dashboard.StopCurrentWorkItem();

            <span style="color: green">// Determine subject of selected item
            </span><span style="color: blue">string </span>subject = <span style="color: blue">string</span>.Empty;
            <span style="color: #2b91af">Explorer </span>explorer = <span style="color: #2b91af">Globals</span>.ThisAddIn.app.ActiveExplorer();
            <span style="color: blue">if </span>(explorer != <span style="color: blue">null </span>&amp;&amp; explorer.Selection != <span style="color: blue">null </span>&amp;&amp; explorer.Selection.Count &gt; 0)
            {
                <span style="color: blue">object </span>item = explorer.Selection[1];
                <span style="color: blue">if </span>(item <span style="color: blue">is </span><span style="color: #2b91af">MailItem</span>)
                {
                    <span style="color: #2b91af">MailItem </span>mailItem = item <span style="color: blue">as </span><span style="color: #2b91af">MailItem</span>;
                    subject = mailItem.Subject;
                }
                <span style="color: blue">if </span>(item <span style="color: blue">is </span><span style="color: #2b91af">TaskItem</span>)
                {
                    <span style="color: #2b91af">TaskItem </span>taskItem = item <span style="color: blue">as </span><span style="color: #2b91af">TaskItem</span>;
                    subject = taskItem.Subject;
                }
                <span style="color: blue">if </span>(item <span style="color: blue">is </span><span style="color: #2b91af">AppointmentItem</span>)
                {
                    <span style="color: #2b91af">AppointmentItem </span>appointmentItem = item <span style="color: blue">as </span><span style="color: #2b91af">AppointmentItem</span>;
                    subject = appointmentItem.Subject;
                }
            }

            
        }
        <span style="color: blue">#endregion

        #region </span>Helpers
        
        <span style="color: blue">private static string </span>GetResourceText(<span style="color: blue">string </span>resourceName)
        {
            <span style="color: #2b91af">Assembly </span>asm = <span style="color: #2b91af">Assembly</span>.GetExecutingAssembly();
            <span style="color: blue">string</span>[] resourceNames = asm.GetManifestResourceNames();
            <span style="color: blue">for </span>(<span style="color: blue">int </span>i = 0; i &lt; resourceNames.Length; ++i)
            {
                <span style="color: blue">if </span>(<span style="color: blue">string</span>.Compare(resourceName, resourceNames[i], <span style="color: #2b91af">StringComparison</span>.OrdinalIgnoreCase) == 0)
                {
                    <span style="color: blue">using </span>(<span style="color: #2b91af">StreamReader </span>resourceReader = <span style="color: blue">new </span><span style="color: #2b91af">StreamReader</span>(asm.GetManifestResourceStream(resourceNames[i])))
                    {
                        <span style="color: blue">if </span>(resourceReader != <span style="color: blue">null</span>)
                        {
                            <span style="color: blue">return </span>resourceReader.ReadToEnd();
                        }
                    }
                }
            }
            <span style="color: blue">return null</span>;
        }

        <span style="color: blue">#endregion
    </span>}
}</pre>
<a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>