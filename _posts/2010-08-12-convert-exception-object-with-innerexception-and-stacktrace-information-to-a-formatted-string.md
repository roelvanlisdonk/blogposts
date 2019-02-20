---
ID: 1666
post_title: >
  Convert Exception object with
  InnerException and StackTrace
  information to a formatted string
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/08/12/convert-exception-object-with-innerexception-and-stacktrace-information-to-a-formatted-string/
published: true
post_date: 2010-08-12 08:26:02
---
<p align="left">If you want to log or show the information from an Exception object, you might want to include InnerException and StackTrace information. The following ExceptionInformation class will do just that:</p>  <div align="left">&#160;</div>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Web;
<span style="color: blue">using </span>System.Text;

<span style="color: blue">namespace </span>Rvl.Demo
{
    <span style="color: blue">public class </span><span style="color: #2b91af">ExceptionInformation
    </span>{
        <span style="color: blue">private </span><span style="color: #2b91af">Exception </span>_exception;

        <span style="color: blue">public </span><span style="color: #2b91af">Exception </span>Exception
        {
            <span style="color: blue">get </span>{ <span style="color: blue">return </span>_exception; }
            <span style="color: blue">set </span>{ _exception = <span style="color: blue">value</span>; }
        }

        <span style="color: blue">public override string </span>ToString()
        {
            <span style="color: blue">string </span>result = <span style="color: blue">string</span>.Empty;

            <span style="color: #2b91af">StringBuilder </span>informationBuilder = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);
            <span style="color: blue">while </span>(Exception != <span style="color: blue">null</span>)
            {
                informationBuilder.Append(<span style="color: #2b91af">Environment</span>.NewLine);
                informationBuilder.Append(<span style="color: #a31515">&quot;Message&quot;</span>).Append(<span style="color: #2b91af">Environment</span>.NewLine);
                informationBuilder.AppendFormat(<span style="color: #a31515">&quot;[{0}]&quot;</span>, Exception.Message).Append(<span style="color: #2b91af">Environment</span>.NewLine)<br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; informationBuilder.Append(<span style="color: #2b91af">Environment</span>.NewLine);<br />                informationBuilder.Append(<span style="color: #a31515">&quot;StackTrace&quot;</span>).Append(<span style="color: #2b91af">Environment</span>.NewLine);
                informationBuilder.Append(<span style="color: #a31515">&quot;[&quot;</span>).Append(<span style="color: #2b91af">Environment</span>.NewLine);
                informationBuilder.Append(Exception.StackTrace).Append(<span style="color: #2b91af">Environment</span>.NewLine);
                informationBuilder.Append(<span style="color: #a31515">&quot;]&quot;</span>).Append(<span style="color: #2b91af">Environment</span>.NewLine).Append(<span style="color: #2b91af">Environment</span>.NewLine);
                Exception = Exception.InnerException;
            }
            result = informationBuilder.ToString();

            <span style="color: blue">return </span>result;
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<div align="left">&#160;</div>
<a href="http://11011.net/software/vspaste"></a>

<p align="left"><strong>Usage</strong></p>

<div align="left">
  <pre class="code"><p><span style="color: #2b91af">            Exception </span>exception = <span style="color: blue">new </span><span style="color: #2b91af">Exception</span>();

            <span style="color: blue">try
            </span>{
                <span style="color: blue">throw new </span><span style="color: #2b91af">Exception</span>(<span style="color: #a31515">&quot;This is a test exception&quot;</span>);
            }
            <span style="color: blue">catch </span>(<span style="color: #2b91af">Exception </span>ex)
            {
                exception = ex;
            }

            <span style="color: #2b91af">ExceptionInformation </span>information = <span style="color: blue">new </span><span style="color: #2b91af">ExceptionInformation</span>();
            information.Exception = exception;
            <span style="color: #2b91af">Console</span>.Write(information.ToString());
</p><p>&#160;</p><p>&#160;</p></pre>
</div>
<a href="http://11011.net/software/vspaste"></a>

<p align="left"><strong>Result</strong></p>

<p align="left">Message
  <br />[This is a test exception]

  <br />

  <br />StackTrace

  <br />[

  <br />&#160;&#160;&#160;&#160;&#160; at Rvl.Demo.Test.ExceptionInformationTester.ToStringTest() in C:\Rvl.Demo.Test\ExceptionInformationTester.cs:line 20

  <br />]</p>