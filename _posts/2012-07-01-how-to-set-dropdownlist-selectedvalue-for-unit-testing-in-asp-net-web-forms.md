---
ID: 2747
post_title: >
  How to set DropDownList.SelectedValue
  for unit testing in ASP .NET web forms.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/07/01/how-to-set-dropdownlist-selectedvalue-for-unit-testing-in-asp-net-web-forms/
published: true
post_date: 2012-07-01 22:11:42
---
<p>If you want to set the [SelectedValue] property of a DropDownList in a unit test, you must first add items to the [Items] property of the DropDownList. If you don’t add items, setting the SelectedValue to a value will not persist.</p>  <pre class="code">[<span style="color: #2b91af">TestMethod</span>]
        <span style="color: blue">public void </span>TestMethod1()
        {
            <span style="color: blue">var </span>dropDownList = <span style="color: blue">new </span><span style="color: #2b91af">DropDownList</span>();
            dropDownList.SelectedValue = <span style="color: #a31515">&quot;First item&quot;</span>;
            <span style="color: #2b91af">Assert</span>.AreEqual(<span style="color: blue">string</span>.Empty, dropDownList.SelectedValue);
            dropDownList.Items.Add(<span style="color: #a31515">&quot;First item&quot;</span>);
            <span style="color: #2b91af">Assert</span>.AreEqual(<span style="color: #a31515">&quot;First item&quot;</span>, dropDownList.SelectedValue);
        }</pre>