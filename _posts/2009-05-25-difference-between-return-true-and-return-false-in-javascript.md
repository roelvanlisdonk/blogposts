---
ID: 470
post_title: >
  Difference between return true; and
  return false; in javascript
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/25/difference-between-return-true-and-return-false-in-javascript/
published: true
post_date: 2009-05-25 12:52:10
---
<p>see: <a href="http://bytes.com/groups/javascript/89023-difference-between-return-true-return-false">http://bytes.com/groups/javascript/89023-difference-between-return-true-return-false</a></p>  <p>When you return something from a function, that value gets returned to the   <br />caller. For instance, say I had a method to multiply two numbers. Maybe the    <br />code looks like this: </p>  <p>function multiply(num1, num2) {   <br />return num1 * num2;    <br />}    <br />result = multiply(2, 4); </p>  <p>The function multiply will return the result of it's multiplication to   <br />wherever it was called. The right-hand side of the result assignment is    <br />where the function is called, so that is where the result is returned to.    <br />So, in this case (with the parameters 2 and 4), it is the same as writing    <br />result = 8; </p>  <p>When you are using return true or false with markup, you are indicating   <br />whether or not you want the default action to happen after the javascript    <br />has been executed. An example is needed: </p>  <p>&lt;a href=&quot;somepage.html&quot; onClick=&quot;alert('Hi'); return true;&quot;&gt;Click Me&lt;/a&gt; </p>  <p>When the link is clicked the javascript code for the onClick will run first,   <br />and we get an alert. We have used return true, so that is saying when we    <br />click OK to remove the alert, we do want to run the markup. So in this case    <br />once we click OK to dismiss the alert, we would then be taken to    <br />somepage.html. If we changed that to return false we would get the alert,    <br />but wouldn't go to somepage.html.</p>