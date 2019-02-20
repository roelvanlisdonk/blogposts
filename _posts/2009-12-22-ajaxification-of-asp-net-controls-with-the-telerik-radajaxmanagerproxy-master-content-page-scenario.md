---
ID: 870
post_title: >
  Ajaxification of ASP .NET controls with
  the Telerik RadAjaxManagerProxy (Master
  / Content page scenario)
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/22/ajaxification-of-asp-net-controls-with-the-telerik-radajaxmanagerproxy-master-content-page-scenario/
published: true
post_date: 2009-12-22 10:58:10
---
<p>If you have a ASP .NET web application with a master page and a content page and you want a LinkButton to update a label with AJAX, you can use the Telerik R.A.D. controls:   <br /></p>  <h4>Web.config</h4>  <p><strong></strong>    <br /><strong>configuration &gt; system.web &gt; pages &gt; controls</strong> should contain:    <br />&lt;add tagPrefix=&quot;telerik&quot; namespace=&quot;Telerik.Web.UI&quot; assembly=&quot;Telerik.Web.UI&quot; /&gt; </p>  <p><strong>configuration &gt; system.web &gt; httpHandlers</strong> should contain:    <br />&lt;add path=&quot;Telerik.Web.UI.WebResource.axd&quot; type=&quot;Telerik.Web.UI.WebResource&quot; verb=&quot;*&quot; validate=&quot;false&quot; /&gt; </p>  <p><strong>configuration &gt; system.webServer &gt; handlers</strong> should contain:    <br />&lt;add name=&quot;Telerik_Web_UI_WebResource_axd&quot; path=&quot;Telerik.Web.UI.WebResource.axd&quot; type=&quot;Telerik.Web.UI.WebResource&quot; verb=&quot;*&quot; preCondition=&quot;integratedMode,runtimeVersionv2.0&quot; /&gt;</p>  <h4>Project</h4>  <p>Should reference Telerik.Web.UI   <br /></p>  <h4>Master page</h4>  <pre class="code"><span style="background: #ffee62">&lt;%</span><span style="color: blue">@ </span><span style="color: #a31515">Master </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;Test.master.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;Rvl.HelperTools.Website.Test&quot; </span><span style="background: #ffee62">%&gt;

</span><span style="color: blue">&lt;!</span><span style="color: #a31515">DOCTYPE </span><span style="color: red">html PUBLIC </span><span style="color: blue">&quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot; &quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;&gt;

&lt;</span><span style="color: #a31515">html </span><span style="color: red">xmlns</span><span style="color: blue">=&quot;http://www.w3.org/1999/xhtml&quot; &gt;
&lt;</span><span style="color: #a31515">head </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: #a31515">title</span><span style="color: blue">&gt;</span>Ajaxification with Telerik<span style="color: blue">&lt;/</span><span style="color: #a31515">title</span><span style="color: blue">&gt;
    </span><span style="color: green">&lt;!-- Use a contentplaceholder in the head, for adding styling from within the user controls --&gt;
    </span><span style="color: blue">&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">ContentPlaceHolder </span><span style="color: red">ID</span><span style="color: blue">=&quot;head&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;/&gt;
&lt;/</span><span style="color: #a31515">head</span><span style="color: blue">&gt;
&lt;</span><span style="color: #a31515">body</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">form </span><span style="color: red">id</span><span style="color: blue">=&quot;mainForm&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">ScriptManager </span><span style="color: red">ID</span><span style="color: blue">=&quot;scriptManager&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; /&gt;
        </span><span style="color: green">&lt;!-- One RadAjaxManager for all content pages that use this master page --&gt;
        </span><span style="color: blue">&lt;</span><span style="color: #a31515">telerik</span><span style="color: blue">:</span><span style="color: #a31515">RadAjaxManager </span><span style="color: red">ID</span><span style="color: blue">=&quot;ajaxManager&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; /&gt;
        </span><span style="color: green">&lt;!-- The skin should be set, else the loading panel is not shown --&gt;
        </span><span style="color: blue">&lt;</span><span style="color: #a31515">telerik</span><span style="color: blue">:</span><span style="color: #a31515">RadAjaxLoadingPanel </span><span style="color: red">ID</span><span style="color: blue">=&quot;radAjaxLoadingPanel&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">BackgroundPosition</span><span style="color: blue">=&quot;Center&quot; </span><span style="color: red">Skin</span><span style="color: blue">=&quot;Default&quot; /&gt;
        &lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">ContentPlaceHolder </span><span style="color: red">ID</span><span style="color: blue">=&quot;mainContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; /&gt;
    &lt;/</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">form</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">body</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">html</span><span style="color: blue">&gt;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p><strong>
    <br /></strong>

  <br />

  <br /><strong></strong></p>

<h4>Content page (aspx)</h4>

<pre class="code"><span style="background: #ffee62">&lt;%</span><span style="color: blue">@ </span><span style="color: #a31515">Page </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;TestContent.aspx.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;Rvl.HelperTools.Website.TestContent&quot; </span><span style="color: red">MasterPageFile</span><span style="color: blue">=&quot;~/Test.Master&quot; </span><span style="background: #ffee62">%&gt;
</span><span style="color: blue">&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Content </span><span style="color: red">ID</span><span style="color: blue">=&quot;Content1&quot; </span><span style="color: red">ContentPlaceHolderID</span><span style="color: blue">=&quot;head&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    </span><span style="color: green">&lt;!-- Add a css class to the head of the master page --&gt;
    </span><span style="color: blue">&lt;</span><span style="color: #a31515">style </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot;&gt;
        </span><span style="color: #a31515">.ViewPanel
        </span>{
            <span style="color: red">height</span>: <span style="color: blue">75px</span>;
        }
    <span style="color: blue">&lt;/</span><span style="color: #a31515">style</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Content</span><span style="color: blue">&gt;
&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Content </span><span style="color: red">ID</span><span style="color: blue">=&quot;MainContent&quot; </span><span style="color: red">ContentPlaceHolderID</span><span style="color: blue">=&quot;mainContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    </span><span style="color: green">&lt;!-- Use the RadAjaxManagerProxy instead of the RadAjaxManager on content pages –&gt;<br />    </span><span style="color: green">&lt;!-- Use the RadAjaxLoadingPanel on the master page --&gt; </span><span style="color: blue">&lt;</span><span style="color: #a31515">telerik</span><span style="color: blue">:</span><span style="color: #a31515">RadAjaxManagerProxy </span><span style="color: red">ID</span><span style="color: blue">=&quot;ajaxManagerProxy&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
       &lt;</span><span style="color: #a31515">AjaxSettings</span><span style="color: blue">&gt;
           &lt;</span><span style="color: #a31515">telerik</span><span style="color: blue">:</span><span style="color: #a31515">AjaxSetting </span><span style="color: red">AjaxControlID</span><span style="color: blue">=&quot;changeLinkButton&quot;&gt;
               &lt;</span><span style="color: #a31515">UpdatedControls</span><span style="color: blue">&gt;
                    </span><span style="color: blue">&lt;</span><span style="color: #a31515">telerik</span><span style="color: blue">:</span><span style="color: #a31515">AjaxUpdatedControl </span><span style="color: red">ControlID</span><span style="color: blue">=&quot;viewPanel&quot; </span><span style="color: red">LoadingPanelID</span><span style="color: blue">=&quot;radAjaxLoadingPanel&quot; /&gt;
               &lt;/</span><span style="color: #a31515">UpdatedControls</span><span style="color: blue">&gt;
           &lt;/</span><span style="color: #a31515">telerik</span><span style="color: blue">:</span><span style="color: #a31515">AjaxSetting</span><span style="color: blue">&gt;
       &lt;/</span><span style="color: #a31515">AjaxSettings</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">telerik</span><span style="color: blue">:</span><span style="color: #a31515">RadAjaxManagerProxy</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Panel </span><span style="color: red">ID</span><span style="color: blue">=&quot;viewPanel&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">CssClass</span><span style="color: blue">=&quot;ViewPanel&quot;&gt;
        &lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label </span><span style="color: red">ID</span><span style="color: blue">=&quot;changeLabel&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Default text&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Panel</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Panel </span><span style="color: red">ID</span><span style="color: blue">=&quot;actionPanel&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
        &lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">LinkButton </span><span style="color: red">ID</span><span style="color: blue">=&quot;changeLinkButton&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">onclick</span><span style="color: blue">=&quot;ChangeLinkButton_Click&quot;&gt;</span>Change<span style="color: blue">&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">LinkButton</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Panel</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Content</span><span style="color: blue">&gt;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<br />

<p><strong></strong>

  <br /></p>

<h4>Content page (.cs)</h4>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Threading;

<span style="color: blue">namespace </span>Rvl.HelperTools.Website
{
    <span style="color: blue">public partial class </span><span style="color: #2b91af">TestContent </span>: System.Web.UI.<span style="color: #2b91af">Page
    </span>{
        <span style="color: blue">protected void </span>Page_Load(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {

        }

        <span style="color: blue">protected void </span>ChangeLinkButton_Click(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
            <span style="color: blue">string </span>textChanged = <span style="color: #a31515">&quot;Text changed&quot;</span>;
            <span style="color: blue">string </span>textChangedAgain = <span style="color: #a31515">&quot;Text changed again&quot;</span>;

            <span style="color: blue">string </span>currentText = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}&quot;</span>, changeLabel.Text);
            <span style="color: blue">if </span>(currentText.Equals(textChanged))
            {
                changeLabel.Text = textChangedAgain;
            }
            <span style="color: blue">else
            </span>{
                changeLabel.Text = textChanged;
            }
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>
  <br />

  <br /></p>

<h4>Result</h4>
<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image17.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image_thumb17.png" width="425" height="397" /></a>