---
ID: 2761
post_title: >
  Convert string to bytes and bytes to
  string without encoding
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/07/10/convert-string-to-bytes-and-bytes-to-string-without-encoding/
published: true
post_date: 2012-07-10 16:35:54
---
<p>I wanted to save information found in a file to a database without having to deal with encodings, well I found my solution at </p>  <p><a href="http://stackoverflow.com/questions/472906/net-string-to-byte-array-c-sharp">http://stackoverflow.com/questions/472906/net-string-to-byte-array-c-sharp</a></p>  <p>&#160;</p>  <pre class="code">&#160;&#160;&#160; [<span style="color: #2b91af">TestClass</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">RliResearchTester
    </span>{
        [<span style="color: #2b91af">TestMethod</span>]
        <span style="color: blue">public void </span>Test()
        {
            <span style="color: blue">string </span>input = <span style="color: #a31515">&quot;Hèllo world&quot;</span>;
            <span style="color: blue">byte</span>[] inputBytes = GetBytes(input);
            <span style="color: blue">string </span>output = GetString(inputBytes);
            <span style="color: #2b91af">Assert</span>.AreEqual(input, output);
        }
        <span style="color: blue">public byte</span>[] GetBytes(<span style="color: blue">string </span>str) 
        { 
            <span style="color: blue">byte</span>[] bytes = <span style="color: blue">new byte</span>[str.Length * <span style="color: blue">sizeof</span>(<span style="color: blue">char</span>)];
            System.<span style="color: #2b91af">Buffer</span>.BlockCopy(str.ToCharArray(), 0, bytes, 0, bytes.Length);
            <span style="color: blue">return </span>bytes;
        }
        <span style="color: blue">public string </span>GetString(<span style="color: blue">byte</span>[] bytes) 
        { 
            <span style="color: blue">char</span>[] chars = <span style="color: blue">new char</span>[bytes.Length / <span style="color: blue">sizeof</span>(<span style="color: blue">char</span>)];
            System.<span style="color: #2b91af">Buffer</span>.BlockCopy(bytes, 0, chars, 0, bytes.Length);
            <span style="color: blue">return new string</span>(chars);
        }

    }</pre>