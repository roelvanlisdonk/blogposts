---
ID: 2676
post_title: 'How to do JavaScript unit testing from C# with MSTest and JSTest'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/05/11/how-to-do-javascript-unit-testing-from-c-with-mstest-and-jstest/
published: true
post_date: 2012-05-11 22:47:00
---
<p>I wanted to run regular MSTest unit test written in C# to assert JavaScript code. There are several ways to accomplish this, but in this case I use JSTest.</p>  <p>Just add JSTest to your C# testproject with NuGet, now you can write tests like:</p>  <p>&#160;</p>  <p><font size="4"><strong>Test class</strong></font></p>  <pre class="code"><span style="color: blue">using </span>JSTest;
<span style="color: blue">using </span>JSTest.ScriptLibraries;
<span style="color: blue">using </span>Microsoft.VisualStudio.TestTools.UnitTesting;
<span style="color: blue">using </span>TestProject1.Helpers;

<span style="color: blue">namespace </span>TestProject1
{
    [<span style="color: #2b91af">TestClass</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">UnitTest1
    </span>{
        [<span style="color: #2b91af">TestMethod</span>]
        <span style="color: blue">public void </span>TestMethod1()
        {
            <span style="color: blue">var </span>script = <span style="color: blue">new </span><span style="color: #2b91af">TestScript</span>();

            <span style="color: green">// Arrange: Append the JavaScript code to test.
            </span><span style="color: blue">string </span>scriptContents = (<span style="color: blue">new </span><span style="color: #2b91af">AssemblyHelper</span>().GetContentsEmbededResourceFile(<span style="color: #a31515">&quot;TestProject1.MvcApplication1.Scripts.Person.js&quot;</span>));
            script.AppendBlock(scriptContents);

            <span style="color: green">// Arrange: Append the JSTest asser library, so we can assert the test code.
            </span>script.AppendBlock(<span style="color: blue">new </span><span style="color: #2b91af">JsAssertLibrary</span>());

            <span style="color: green">// Append &quot;Act&quot; JavaScript code.
            </span>script.AppendBlock(<span style="color: #a31515">&quot;var person1 = new Person('John Do', 32, 'Software Engineer');&quot;</span>);

            <span style="color: green">// Assert.
            </span>script.RunTest(<span style="color: #a31515">@&quot;assert.equal('Jonh Do test', person1.sayName());&quot;</span>);
        }
    }
}</pre>

<p>Running this test within Microsoft Visual Studio 2010 will result in a passed test.</p>

<p>&#160;</p>

<p><font size="4"><strong>JavaScript code to test</strong></font>

  <br />

  <br /></p>

<p>
  <pre class="code"><span style="color: blue">function </span>Person(name, age, job)
{
    <span style="color: blue">var </span>privateField1 = <span style="color: maroon">'test'</span>;
    <span style="color: blue">this</span>.name = name;
    <span style="color: blue">this</span>.age = age;
    <span style="color: blue">this</span>.job = job;
    <span style="color: blue">this</span>.privilegedMethod = <span style="color: blue">function </span>() { <span style="color: blue">return </span>privateField1; }
};

Person.prototype.sayName = <span style="color: blue">function </span>()
{
    <span style="color: blue">return this</span>.name + <span style="color: maroon">' ' </span>+ <span style="color: blue">this</span>.privilegedMethod();
};</pre>
</p>

<p><strong><font size="4">Notes</font></strong>

  <br />- The privilegedMethod is used to access private fields on the Person class.

  <br />- You can set breakpoints in the JavaScript code!!

  <br />

  <br /></p>

<p><font size="4"><strong>C# helper class</strong></font></p>

<p>
  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.IO;
<span style="color: blue">using </span>System.Reflection;

<span style="color: blue">namespace </span>TestProject1.Helpers
{
    <span style="color: blue">public class </span><span style="color: #2b91af">AssemblyHelper
    </span>{
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Read the contents of an embededresourcefile with the given name.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;resourceName&quot;&gt;</span><span style="color: green">Name of the resource.</span><span style="color: gray">&lt;/param&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color: blue">public string </span>GetContentsEmbededResourceFile(<span style="color: blue">string </span>resourceName)
        {
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrWhiteSpace(resourceName)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;resourceName&quot;</span>); }

            <span style="color: blue">string </span>contents = <span style="color: blue">string</span>.Empty;
            <span style="color: blue">using </span>(<span style="color: #2b91af">Stream </span>stream = <span style="color: #2b91af">Assembly</span>.GetExecutingAssembly().GetManifestResourceStream(resourceName))
            <span style="color: blue">using </span>(<span style="color: blue">var </span>reader = <span style="color: blue">new </span><span style="color: #2b91af">StreamReader</span>(stream))
            {
                contents = reader.ReadToEnd();
            }
            <span style="color: blue">return </span>contents;
        }
    }
}</pre>
</p>



<p><font size="4"><strong>Microsoft Visual Studio 2010</strong></font>

  <br /></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/05/image7.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/05/image_thumb7.png" width="385" height="902" /></a></p>