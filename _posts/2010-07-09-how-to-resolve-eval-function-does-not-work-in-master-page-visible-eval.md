---
ID: 1598
post_title: "How to resolve: Eval function does not work in master page, visible='&lt;%# Eval(&hellip;) %&gt;&#8217;"
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/07/09/how-to-resolve-eval-function-does-not-work-in-master-page-visible-eval/
published: true
post_date: 2010-07-09 11:54:19
---
<p>If you want to set the visibility of a control based on some C# code like User.IsInRole(&quot;Administrator&quot;) directly in your *.aspx page, you can use the data binding syntax &lt;%# … %&gt; in the ASP .NET page. You don’t need the Eval function, but you do need to bind you’re page, else the code in&#160; &lt;%# … %&gt; will not be executed.   <br /></p>  <p>If you use the &lt;%# … %&gt; syntax in your master page, you should call this.DataBind() in your Page_Load event, else the code in &lt;%# … %&gt; won’t be executed.</p>  <p><strong>*.ASPX</strong></p>  <pre class="code"><span style="background: yellow">&lt;%</span><span style="color: blue">@ </span><span style="color: maroon">Master  </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;Site.master.cs&quot; 
            </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;Rvl.Demo.AspNet4.EF.WebApplication.SiteMaster&quot; </span><span style="background: yellow">%&gt;

</span><span style="color: blue">&lt;!</span><span style="color: maroon">DOCTYPE </span><span style="color: red">html PUBLIC </span><span style="color: blue">&quot;-//W3C//DTD XHTML 1.0 Strict//EN&quot; &quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd&quot;&gt;
&lt;</span><span style="color: maroon">html </span><span style="color: red">xmlns</span><span style="color: blue">=&quot;http://www.w3.org/1999/xhtml&quot; </span><span style="color: red">xml</span><span style="color: blue">:</span><span style="color: red">lang</span><span style="color: blue">=&quot;en&quot;&gt;
&lt;</span><span style="color: maroon">head </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: maroon">title</span><span style="color: blue">&gt;&lt;/</span><span style="color: maroon">title</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">link </span><span style="color: red">href</span><span style="color: blue">=&quot;~/Styles/Site.css&quot; </span><span style="color: red">rel</span><span style="color: blue">=&quot;stylesheet&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot; /&gt;
    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">ContentPlaceHolder </span><span style="color: red">ID</span><span style="color: blue">=&quot;HeadContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">ContentPlaceHolder</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">head</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">body</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">form </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;page&quot;&gt;
        &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton </span><span style="color: red">ID</span><span style="color: blue">=&quot;LinkButton1&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; 
        </span><span style="color: red">Visible</span><span style="color: blue">='</span><span style="background: yellow">&lt;%</span><span style="color: blue"># </span>User.IsInRole(&quot;Administrator&quot;) <span style="background: yellow">%&gt;</span><span style="color: blue">'&gt;</span>This link will only be visible for Administrators<span style="color: blue">&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton</span><span style="color: blue">&gt;</span><span style="color: blue">       
    &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: maroon">form</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">body</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">html</span><span style="color: blue">&gt;

</span></pre>
<a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>

<p><strong>*.cs</strong></p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Web;
<span style="color: blue">using </span>System.Web.UI;
<span style="color: blue">using </span>System.Web.UI.WebControls;

<span style="color: blue">namespace </span>Rvl.Demo.AspNet4.EF.WebApplication
{
    <span style="color: blue">public partial class </span><span style="color: #2b91af">SiteMaster </span>: System.Web.UI.<span style="color: #2b91af">MasterPage
    </span>{
        <span style="color: blue">protected void </span>Page_Load(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
            <span style="color: blue">this</span>.DataBind();
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>