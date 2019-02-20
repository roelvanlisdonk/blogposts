---
ID: 687
post_title: 'Best Practices &#8211; CSS'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/09/13/best-practices-css/
published: true
post_date: 2009-09-13 20:05:38
---
<p>This post describes a code guidelines and a best practices for CSS, it will evolve over time and will be updated whenever I find new or better best practices.</p>  <p><strong>CSS Files</strong></p>  <ul>   <li>Every web application should have a General.css, which contains only the classes that are used in more then 1 page or user control. </li>    <li>Every master page, page, user control, external library components should have there own css file. </li>    <li>Create a browser specific css file, if you have to use browser specific css hacks </li>    <li>All css files should be saved in a Css folder in the root of the web application. </li>    <li>The master page should first link to the General.css and then to the Master.css and then it should contain a contentplaceholder, so pages and user controls can add there css file to the head of the master page&#160; </li>    <pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">ContentPlaceHolder </span><span style="color: red">ID</span><span style="color: blue">=&quot;head&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">ContentPlaceHolder</span><span style="color: blue">&gt;</span></pre>
  <a href="http://11011.net/software/vspaste"></a>

  <li>All pages and user controls should link to there own css file, by adding a link to there css file in the master page by implementing the contentplaceholder head from the master page: </li>

  <pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Content </span><span style="color: red">ID</span><span style="color: blue">=&quot;Content1&quot; </span><span style="color: red">ContentPlaceHolderID</span><span style="color: blue">=&quot;head&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: #a31515">link </span><span style="color: red">href</span><span style="color: blue">=&quot;Css\Default.css&quot; </span><span style="color: red">rel</span><span style="color: blue">=&quot;Stylesheet&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot; /&gt;
&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Content</span><span style="color: blue">&gt;</span></pre>
  <a href="http://11011.net/software/vspaste"></a>

  <li>&#160;</li>
</ul>

<p>&#160;</p>

<p><strong>CSS Structure</strong></p>

<ul>
  <li>Keep HTML free of presentational attributes, all styling should go in classes in css files.</li>

  <li>Every class defined in CSS should be used, else it must be removed. </li>

  <li>Every browser specific hack should be commented. </li>

  <li>Don´t use a reset scripts except for padding and margin when working with a pixel perfect design, else external libraries might no work. </li>

  <li>Don´t use css direct on html tags, only on html and body tag, all other tags should have classes, else external libraries might no work. </li>

  <li>Don´t use important! only if you have to overwrite inline styling and then comment it. </li>

  <li>Class name should start with lowercase and use camel casing. </li>

  <li>Use only classes and avoid id´s, because asp .net will render a control in a usercontrol like ctrl001.</li>

  <li>Order the classes within the css file based on the order of the markup. If the first element of the page is an &lt;h1 class=&quot;titleHeader&quot;&gt;, put it first.</li>

  <li>Properties within a class should be in alphabetic order.</li>

  <li>Set the font on the body tag, so other tags inherit from it.</li>

  <li>Set classes on outer elements and use selectors to style the child elements.</li>

  <li>Don’ t use * before property name, so don’ t use .exampleClass { *width: 20px; }</li>
</ul>

<p><strong>CSS Tips</strong></p>

<ul>
  <li>If you want to add horizontal spacing between rows, use a border for the &lt;tr&gt; tag:</li>

  <pre class="code"><span style="color: #a31515">.rowWithBottomSpacing
</span>{
    <span style="color: red">border-bottom</span>: <span style="color: blue">solid 5px #ffffff</span>;
}</pre>
  <a href="http://11011.net/software/vspaste"></a>

  <li>An example IE8 hack could be, a class that hides the dashed border arround a link when it’ s clicked:</li>

  <pre class="code"><span style="color: #a31515">.linkWithNoDashesOnActivation
</span>{
    <span style="color: red">border-color</span>: <span style="color: blue">Red</span>;
    <span style="color: red">border-style</span>: <span style="color: blue">solid</span>;
    <span style="color: red">border-width</span>: <span style="color: blue">1px</span>;
    <span style="color: red">color</span>: <span style="color: blue">#000000</span>;
    <span style="color: red">display</span>: <span style="color: blue">block</span>;
    <span style="color: red">outline</span>: <span style="color: blue">none</span>;
} </pre>

  <li>Note: a:hover MUST come after a:link and a:visited in the CSS definition in order to be effective.</li>

  <li>Note: a:active MUST come after a:hover in the CSS definition in order to be effective.</li>

  <li>Note: Pseudo-class names are not case-sensitive.</li>

  <pre class="code"><span style="color: #a31515">a:link </span>{<span style="color: red">color</span>:<span style="color: blue">#FF0000</span>}      <span style="color: green">/* unvisited link */
</span><span style="color: #a31515">a:visited </span>{<span style="color: red">color</span>:<span style="color: blue">#00FF00</span>}  <span style="color: green">/* visited link */
</span><span style="color: #a31515">a:hover </span>{<span style="color: red">color</span>:<span style="color: blue">#FF00FF</span>}  <span style="color: green">/* mouse over link */
</span><span style="color: #a31515">a:active </span>{<span style="color: red">color</span>:<span style="color: blue">#0000FF</span>}  <span style="color: green">/* selected link */
</span><span style="color: #a31515">a:focus </span>{<span style="color: red">color</span>:<span style="color: blue">#00A0FF</span>}  <span style="color: green">/* focused link */</span></pre>
  <a href="http://11011.net/software/vspaste"></a>

  <li>&#160;</li>
</ul>

<p>
  <br /><strong>Source and Related posts</strong></p>

<ul>
  <li><a title="http://www.w3.org/TR/CSS21/" href="http://www.w3.org/TR/CSS21/">http://www.w3.org/TR/CSS21/</a></li>

  <li><a title="http://www.smashingmagazine.com/2007/05/10/70-expert-ideas-for-better-css-coding/" href="http://www.smashingmagazine.com/2007/05/10/70-expert-ideas-for-better-css-coding/">http://www.smashingmagazine.com/2007/05/10/70-expert-ideas-for-better-css-coding/</a></li>
</ul>

<p>
  <br />

  <br />

  <br />

  <br />

  <br />

  <br />

  <br /></p>

<p>&#160;</p>

<p><a href="http://11011.net/software/vspaste">&#160;</a></p>