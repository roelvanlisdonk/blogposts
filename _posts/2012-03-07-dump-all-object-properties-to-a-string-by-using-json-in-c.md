---
ID: 2525
post_title: 'Dump all object properties to a string by using JSON in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/03/07/dump-all-object-properties-to-a-string-by-using-json-in-c/
published: true
post_date: 2012-03-07 13:12:36
---
<p>If you want to dump the properties of an object into a string (lets say for logging purposes), you can use JSON serialization in C#. The output string is far less bulky than using XML serialization.</p>   <pre class="code"><span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Web.Script.Serialization;
<span style="color: blue">using </span>Microsoft.VisualStudio.TestTools.UnitTesting;

<span style="color: blue">namespace </span>NewCode.Rli
{
    [<span style="color: #2b91af">TestClass</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">NewCodeTester
    </span>{
        [<span style="color: #2b91af">TestMethod</span>]
        <span style="color: blue">public void </span>Test()
        {
            <span style="color: blue">var </span>person = <span style="color: blue">new </span><span style="color: #2b91af">Person
            </span>{
                FirstName = <span style="color: #a31515">&quot;John&quot;</span>,
                Kids = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">Person</span>&gt;
                {
                    <span style="color: blue">new </span><span style="color: #2b91af">Person </span>{ FirstName = <span style="color: #a31515">&quot;Kid&quot;</span>, LastName = <span style="color: #a31515">&quot;One&quot;</span>},
                    <span style="color: blue">new </span><span style="color: #2b91af">Person </span>{ FirstName = <span style="color: #a31515">&quot;Kid&quot;</span>, LastName = <span style="color: #a31515">&quot;Two&quot;</span>}
                },
                LastName = <span style="color: #a31515">&quot;Do&quot;</span>,
            };
            <span style="color: blue">var </span>serializer = <span style="color: blue">new </span><span style="color: #2b91af">JavaScriptSerializer</span>();
            <span style="color: blue">string </span>output = serializer.Serialize(person);

            <span style="color: green">/* Output: 
              {
               &quot;FirstName&quot;:&quot;John&quot;,
               &quot;LastName&quot;:&quot;Do&quot;,
               &quot;Kids&quot;:
               [
                   {
                       &quot;FirstName&quot;:&quot;Kid&quot;,
                       &quot;LastName&quot;:&quot;One&quot;,
                       &quot;Kids&quot;:null
                   },
                   {
                       &quot;FirstName&quot;:&quot;Kid&quot;,
                       &quot;LastName&quot;:&quot;Two&quot;,
                       &quot;Kids&quot;:null
                   }
              ]
             }
           */
        </span>}
    }
    <span style="color: blue">public class </span><span style="color: #2b91af">Person
    </span>{
        <span style="color: blue">public string </span>FirstName { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public string </span>LastName { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public </span><span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">Person</span>&gt; Kids { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
    }
}</pre>