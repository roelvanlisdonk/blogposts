---
ID: 3679
post_title: >
  Casting when dealing with nullable
  fields in a SqlDataReader
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/01/24/casting-when-dealing-with-nullable-fields-in-a-sqldatareader/
published: true
post_date: 2014-01-24 14:04:13
---
<p>When dealing with nullable fields in a SqlDataReader, use:</p>   <pre class="code"><span style="background: white; color: blue">int</span><span style="background: white; color: black">? field_a = reader[</span><span style="background: white; color: #a31515">&quot;field_a&quot;</span><span style="background: white; color: black">] </span><span style="background: white; color: blue">as int</span><span style="background: white; color: black">?;
</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">field_b = reader[</span><span style="background: white; color: #a31515">&quot;field_a&quot;</span><span style="background: white; color: black">] </span><span style="background: white; color: blue">as string</span><span style="background: white; color: black">;</span></pre>

<p>instead of:</p>

<p>
  <pre class="code"><span style="background: white; color: blue">int</span><span style="background: white; color: black">? field_a = </span><span style="background: white; color: #2b91af">Convert</span><span style="background: white; color: black">.ToInt32(reader[</span><span style="background: white; color: #a31515">&quot;field_a&quot;</span><span style="background: white; color: black">]);
</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">field_b = </span><span style="background: white; color: #2b91af">Convert</span><span style="background: white; color: black">.ToString(reader[</span><span style="background: white; color: #a31515">&quot;field_a&quot;</span><span style="background: white; color: black">]);</span></pre>
  <a title="http://stackoverflow.com/questions/2141575/how-to-efficiently-convert-cast-a-sqldatareader-field-to-its-corresponding" href="http://stackoverflow.com/questions/2141575/how-to-efficiently-convert-cast-a-sqldatareader-field-to-its-corresponding">http://stackoverflow.com/questions/2141575/how-to-efficiently-convert-cast-a-sqldatareader-field-to-its-corresponding</a></p>