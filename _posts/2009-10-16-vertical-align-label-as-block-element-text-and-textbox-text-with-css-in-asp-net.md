---
ID: 768
post_title: >
  Vertical align label (as block element)
  text and textbox text with CSS in ASP
  .NET
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/16/vertical-align-label-as-block-element-text-and-textbox-text-with-css-in-asp-net/
published: true
post_date: 2009-10-16 20:39:01
---
<p>If you use a label and an input element as block element with CSS, you can’t use vertical-align, border-top, padding-top or margin-top for vertical alignment of the text values.&#160;&#160; <br />    <br />    <br />    <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/10/image6.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/10/image_thumb6.png" width="244" height="132" /></a>     <br />    <br />    <br /></p>  <pre class="code"><span style="background: #ffee62">&lt;%</span><span style="color: blue">@ </span><span style="color: #a31515">Page </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;Default.aspx.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;Rvl.HelperTools.Website._Default&quot; </span><span style="background: #ffee62">%&gt;

</span><span style="color: blue">&lt;!</span><span style="color: #a31515">DOCTYPE </span><span style="color: red">html PUBLIC </span><span style="color: blue">&quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot; &quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;&gt;

&lt;</span><span style="color: #a31515">html </span><span style="color: red">xmlns</span><span style="color: blue">=&quot;http://www.w3.org/1999/xhtml&quot;&gt;
&lt;</span><span style="color: #a31515">head </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: #a31515">title</span><span style="color: blue">&gt;</span>Untitled Page<span style="color: blue">&lt;/</span><span style="color: #a31515">title</span><span style="color: blue">&gt;

    </span><span style="color: green">&lt;!-- Load css styles --&gt;
    </span><span style="color: blue">&lt;</span><span style="color: #a31515">style </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot;&gt;
        </span><span style="color: #a31515">.Main
        </span>{
            <span style="color: red">background-color</span>: <span style="color: blue">white</span>;
            <span style="color: red">margin-left</span>: <span style="color: blue">auto</span>; <span style="color: green">/* Center mainTable for &gt;= IE6  */
            </span><span style="color: red">margin-right</span>: <span style="color: blue">auto</span>; <span style="color: green">/* Center mainTable for &gt;= IE6  */
        </span>}
        <span style="color: #a31515">.LeftLabelColumn
        </span>{
            <span style="color: red">display</span>: <span style="color: blue">block</span>;
            <span style="color: red">margin-left</span>: <span style="color: blue">10px</span>;
            <span style="color: red">margin-right</span>: <span style="color: blue">10px</span>;
            <span style="color: red">height</span>: <span style="color: blue">22px</span>;
            <span style="color: red">padding-top</span>: <span style="color: blue">5px</span>;
        }
        <span style="color: #a31515">.LeftValueColumn
        </span>{
            <span style="color: red">display</span>: <span style="color: blue">block</span>;
            <span style="color: red">margin-left</span>: <span style="color: blue">10px</span>;
            <span style="color: red">margin-right</span>: <span style="color: blue">10px</span>;
        }
    <span style="color: blue">&lt;/</span><span style="color: #a31515">style</span><span style="color: blue">&gt;

    &lt;</span><span style="color: #a31515">script </span><span style="color: red">language</span><span style="color: blue">=&quot;javascript&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/javascript&quot;&gt;
    &lt;/</span><span style="color: #a31515">script</span><span style="color: blue">&gt;

&lt;/</span><span style="color: #a31515">head</span><span style="color: blue">&gt;
&lt;</span><span style="color: #a31515">body</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">form </span><span style="color: red">id</span><span style="color: blue">=&quot;form1&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: #a31515">div </span><span style="color: red">class</span><span style="color: blue">=&quot;Main&quot;&gt;
        &lt;</span><span style="color: #a31515">div </span><span style="color: red">style</span><span style="color: blue">=&quot;</span><span style="color: red">float</span>: <span style="color: blue">left</span>; <span style="color: red">border-top</span>: <span style="color: blue">solid 1px white</span>;<span style="color: blue">&quot;&gt;
            &lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label </span><span style="color: red">ID</span><span style="color: blue">=&quot;Label1&quot; </span><span style="color: red">CssClass</span><span style="color: blue">=&quot;LeftLabelColumn&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Customer&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label </span><span style="color: red">ID</span><span style="color: blue">=&quot;Label2&quot; </span><span style="color: red">CssClass</span><span style="color: blue">=&quot;LeftLabelColumn&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;City&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label </span><span style="color: red">ID</span><span style="color: blue">=&quot;Label3&quot; </span><span style="color: red">CssClass</span><span style="color: blue">=&quot;LeftLabelColumn&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Supplier&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label </span><span style="color: red">ID</span><span style="color: blue">=&quot;Label4&quot; </span><span style="color: red">CssClass</span><span style="color: blue">=&quot;LeftLabelColumn&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Products&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
        </span><span style="color: green">&lt;!-- Because we can't use border-top, margin-top or padding-top on a textbox, we surround the textboxes with div tags --&gt;
        </span><span style="color: blue">&lt;</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">div </span><span style="color: red">style</span><span style="color: blue">=&quot;</span><span style="color: red">padding-top</span>: <span style="color: blue">5px</span>;<span style="color: blue">&quot;&gt;&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox </span><span style="color: red">ID</span><span style="color: blue">=&quot;TextBox1&quot; </span><span style="color: red">CssClass</span><span style="color: blue">=&quot;LeftValueColumn&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Microsoft&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">div </span><span style="color: red">style</span><span style="color: blue">=&quot;</span><span style="color: red">padding-top</span>: <span style="color: blue">5px</span>;<span style="color: blue">&quot;&gt;&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox </span><span style="color: red">ID</span><span style="color: blue">=&quot;TextBox2&quot; </span><span style="color: red">CssClass</span><span style="color: blue">=&quot;LeftValueColumn&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Redmond&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">div </span><span style="color: red">style</span><span style="color: blue">=&quot;</span><span style="color: red">padding-top</span>: <span style="color: blue">5px</span>;<span style="color: blue">&quot;&gt;&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox </span><span style="color: red">ID</span><span style="color: blue">=&quot;TextBox3&quot; </span><span style="color: red">CssClass</span><span style="color: blue">=&quot;LeftValueColumn&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;IBM&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">div </span><span style="color: red">style</span><span style="color: blue">=&quot;</span><span style="color: red">padding-top</span>: <span style="color: blue">5px</span>;<span style="color: blue">&quot;&gt;&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox </span><span style="color: red">ID</span><span style="color: blue">=&quot;TextBox4&quot; </span><span style="color: red">CssClass</span><span style="color: blue">=&quot;LeftValueColumn&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Windows, Office&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">form</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">body</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">html</span><span style="color: blue">&gt;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>