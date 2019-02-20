---
ID: 781
post_title: >
  Open networkshare with a LinkButton by
  setting the href attribute of LinkButton
  with code behind.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/28/open-networkshare-with-a-linkbutton-by-setting-the-href-attribute-of-linkbutton-with-code-behind/
published: true
post_date: 2009-10-28 11:14:16
---
<p>If you want to open a network share with a LinkButton, you can set it’s href attribute manually with code behind:   <br />    <br /></p>  <pre class="code"><span style="background: #ffee62">&lt;%</span><span style="color: blue">@ </span><span style="color: #a31515">Page </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;Test.aspx.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;Rvl.HelperTools.Website.Test&quot; </span><span style="background: #ffee62">%&gt;

</span><span style="color: blue">&lt;!</span><span style="color: #a31515">DOCTYPE </span><span style="color: red">html PUBLIC </span><span style="color: blue">&quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot; &quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;&gt;

&lt;</span><span style="color: #a31515">html </span><span style="color: red">xmlns</span><span style="color: blue">=&quot;http://www.w3.org/1999/xhtml&quot; &gt;
&lt;</span><span style="color: #a31515">head </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: #a31515">title</span><span style="color: blue">&gt;</span>Untitled Page<span style="color: blue">&lt;/</span><span style="color: #a31515">title</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">head</span><span style="color: blue">&gt;
&lt;</span><span style="color: #a31515">body</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">form </span><span style="color: red">id</span><span style="color: blue">=&quot;form1&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">LinkButton </span><span style="color: red">ID</span><span style="color: blue">=&quot;LinkButton1&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;</span>Show network share with LinkButton<span style="color: blue">&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">LinkButton</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">a </span><span style="color: red">href</span><span style="color: blue">=&quot;\\Myshare&quot; </span><span style="color: red">id</span><span style="color: blue">=&quot;showReportsButton&quot;&gt;</span>Show network share with Link<span style="color: blue">&lt;/</span><span style="color: #a31515">a</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">form</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">body</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">html</span><span style="color: blue">&gt;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>
  <br /></p>

<pre class="code"><span style="color: gray">        /// &lt;summary&gt;
        /// </span><span style="color: green">Event fires on pageload
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;sender&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;e&quot;&gt;&lt;/param&gt;
        </span><span style="color: blue">protected void </span>Page_Load(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
            <span style="color: blue">this</span>.LinkButton1.Attributes[<span style="color: #a31515">&quot;href&quot;</span>] = <span style="color: #a31515">@&quot;\\Myshare&quot;</span>;

        }</pre>
<a href="http://11011.net/software/vspaste"></a>