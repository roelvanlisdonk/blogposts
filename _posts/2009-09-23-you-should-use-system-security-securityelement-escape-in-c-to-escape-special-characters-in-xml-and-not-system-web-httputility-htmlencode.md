---
ID: 716
post_title: 'You should use System.Security.SecurityElement.Escape in C# to escape special characters in XML and not System.Web.HttpUtility.HtmlEncode'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/09/23/you-should-use-system-security-securityelement-escape-in-c-to-escape-special-characters-in-xml-and-not-system-web-httputility-htmlencode/
published: true
post_date: 2009-09-23 14:14:43
---
<p>You should use the function System.Security.SecurityElement.Escape and not the function System.Web.HttpUtility.HtmlEncode to escape special characters in XML if you don’t want the characters like éûÉ to be converted to &amp;#233;&amp;#251;&amp;#201; which is permit able but not necessary en can result in long xml fields.</p>  <pre class="code"><span style="color: blue">var </span>escapedXml = System.Security.<span style="color: #2b91af">SecurityElement</span>.Escape(<span style="color: #a31515">@&quot;&amp;&lt;&gt;'&quot;&quot;’éûÉغ&quot;</span>);
<span style="color: #2b91af">Console</span>.WriteLine(escapedXml);
<span style="color: green">// Result=&amp;amp;&amp;lt;&amp;gt;&amp;apos;&amp;quot;’éûÉغ

</span>escapedXml = System.Web.<span style="color: #2b91af">HttpUtility</span>.HtmlEncode(<span style="color: #a31515">@&quot;&amp;&lt;&gt;'&quot;&quot;’éûÉغ&quot;</span>);
<span style="color: #2b91af">Console</span>.WriteLine(escapedXml);
<span style="color: green">// Result=&amp;amp;&amp;lt;&amp;gt;'&amp;quot;’&amp;#233;&amp;#251;&amp;#201;غ</span></pre>

<p>
  <br /></p>

<p>To revert the escape process, use:</p>

<pre class="code"><span style="color: #2b91af">SecurityElement </span>securityElement = System.Security.<span style="color: #2b91af">SecurityElement</span>.FromString(<span style="color: #a31515">&quot;&lt;test&gt;H&amp;amp;M&lt;/test&gt;&quot;</span>);
<span style="color: blue">string </span>unescapedText = securityElement.Text;
<span style="color: #2b91af">Console</span>.WriteLine(unescapedText); <span style="color: green">// Result: H&amp;M
</span></pre>

<p>Or</p>

<pre class="code"><span style="color: green">// Data is the un-escaped text that should be inserted in a XML tag.
</span><span style="color: blue">string </span>data = <span style="color: #a31515">&quot;H&amp;amp;M&quot;</span>;

<span style="color: green">// A xml tag with the name &quot;test&quot; is used, just for creating the SecurityElement.
</span><span style="color: blue">var </span>securityElement = <span style="color: blue">new </span><span style="color: #2b91af">SecurityElement</span>(<span style="color: #a31515">&quot;test&quot;</span>, data);

<span style="color: green">// Generate the un-escaped text.
</span><span style="color: blue">string </span>unescapedText = securityElement.Text;

<span style="color: green">// Result: H&amp;M
</span><span style="color: #2b91af">Console</span>.WriteLine(unescapedText);</pre>

<p>Or use the InnerText property of a XmlNode:</p>

<pre class="code"><span style="color: green">// Data is the un-escaped text that should be inserted in a XML tag.
</span><span style="color: blue">string </span>data = <span style="color: #a31515">&quot;H&amp;amp;M&quot;</span>;
 
<span style="color: #2b91af">XmlDocument </span>document = <span style="color: blue">new </span><span style="color: #2b91af">XmlDocument</span>();
document.LoadXml(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;&lt;test&gt;{0}&lt;/test&gt;&quot;</span>, data));
<span style="color: #2b91af">XmlNode </span>node = document.DocumentElement.FirstChild;

<span style="color: green">// Generate the un-escaped text.
</span><span style="color: blue">string </span>unescapedText = node.InnerText;

<span style="color: green">// Result: H&amp;M
</span><span style="color: #2b91af">Console</span>.WriteLine(unescapedText);</pre>