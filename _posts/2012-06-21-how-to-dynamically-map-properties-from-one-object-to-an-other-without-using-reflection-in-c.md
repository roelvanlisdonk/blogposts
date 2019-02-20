---
ID: 2739
post_title: 'How to create a generic property mapper, that maps properties from one object to an other, without relying on inheritance, composition or reflection in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/06/21/how-to-dynamically-map-properties-from-one-object-to-an-other-without-using-reflection-in-c/
published: true
post_date: 2012-06-21 21:04:23
---
<p>Lets say you want to generate a generic [PropertyMapper] class, that can map the properties of a TypeX instance to a TypeY instance without introducing inheritance, composition or reflection in C#.</p>  <p>Well you can use several libraries, like automapper etc. but when you want to do this by hand, you can start by looking at the following example. In this example the PropertyMapper class maps the Person.Name property to a TextBox.Text property:</p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Web.UI.WebControls;
<span style="color: blue">using </span>Microsoft.VisualStudio.TestTools.UnitTesting;

<span style="color: blue">namespace </span>Rli.Research.Test
{
    <span style="color: blue">public class </span><span style="color: #2b91af">PropertyMapper
    </span>{
        <span style="color: blue">public void </span>Map&lt;TSource, TDestination&gt;(TSource source, TDestination destination, <span style="color: #2b91af">Action</span>&lt;TSource, TDestination&gt; mapAction)
        {
            mapAction(source, destination);
        }
    }
    <span style="color: blue">public class </span><span style="color: #2b91af">Person
    </span>{
        <span style="color: blue">public string </span>Name { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
    }
    [<span style="color: #2b91af">TestClass</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">UnitTester
    </span>{
        [<span style="color: #2b91af">TestMethod</span>]
        <span style="color: blue">public void </span>Map_should_copy_the_contents_of_the_property_person_name_to_the_textbox_text_property()
        {
            <span style="color: green">// Arrange.
            </span><span style="color: blue">var </span>source = <span style="color: blue">new </span><span style="color: #2b91af">TextBox</span>();
            <span style="color: blue">var </span>destination = <span style="color: blue">new </span><span style="color: #2b91af">Person </span>{ Name = <span style="color: #a31515">&quot;John Do&quot; </span>};
            <span style="color: #2b91af">Action</span>&lt;<span style="color: #2b91af">TextBox</span>, <span style="color: #2b91af">Person</span>&gt; mapAction = (source1, destination1) =&gt; source1.Text = destination1.Name;

            <span style="color: green">// Act.
            </span><span style="color: blue">var </span>mapper = <span style="color: blue">new </span><span style="color: #2b91af">PropertyMapper</span>();
            mapper.Map(source, destination, mapAction);

            <span style="color: green">// Assert.
            </span><span style="color: #2b91af">Assert</span>.AreEqual(destination.Name, source.Text);
        }
    }
}</pre>


<p> The unit test will succeed.</p>

<p>&#160;</p>

<p><strong>Generic TypeConverter</strong></p>

<p>Of course you can map multiple properties in one &quot;mapAction”, allowing to &quot;convert&quot; one type to an other, without relying on inheritance composition or reflection.</p>

<p>&#160;</p>

<p><strong>Note</strong></p>

<p>This code is <strong>not</strong> intended to be used for model to view binding, for this please use INotifyPropertyChanged and CallerInfoAttributes in C# 5.0: <a href="http://awkwardcoder.blogspot.nl/2012/03/how-fast-is-callerinfoattributes-for.html">http://awkwardcoder.blogspot.nl/2012/03/how-fast-is-callerinfoattributes-for.html</a></p>