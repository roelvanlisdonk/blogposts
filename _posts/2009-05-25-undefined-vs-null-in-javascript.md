---
ID: 469
post_title: undefined vs null in javascript
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/25/undefined-vs-null-in-javascript/
published: true
post_date: 2009-05-25 12:50:15
---
<div class="padten">   <div class="ms-inputuserfield padfive seventyp">     <div>       <div class="ExternalClass6FA9DD297AC04BDD8F8FD12B59EF0E56">         <p>There is a difference between a varaible declarde as:</p>          <p>var test;</p>          <p>and a variable declared as:</p>          <p>var test = null;</p>          <p>The first variable has a value of undefined whereas the second variable has a value of null;           <br />Code example:</p>          <pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">script </span><span style="color: red">type</span><span style="color: blue">=&quot;text/javascript&quot;&gt;
        var </span>test;
        <span style="color: blue">if</span>(test == <span style="color: blue">null</span>)
        {
            alert(<span style="color: #a31515">&quot;The variable [test] equals [undefined] or [null]&quot;</span>);
        }
        <span style="color: blue">var </span>test1 = <span style="color: blue">null</span>;
        <span style="color: blue">if</span>(test1 == <span style="color: blue">null</span>)
        {
            alert(<span style="color: #a31515">&quot;The variable [test1] equals [undefined] or [null]&quot;</span>);
        }
        <span style="color: blue">var </span>test2 = <span style="color: blue">null</span>;
        <span style="color: blue">if</span>(test2 === <span style="color: blue">null</span>)
        {
            alert(<span style="color: #a31515">&quot;The variable [test2] equals [null] and not [undefined], because we use the operator [===] and not [==]&quot;</span>);
        }
        <span style="color: blue">var </span>test3;
        <span style="color: blue">if</span>(test3 === undefined)
        {
            alert(<span style="color: #a31515">&quot;The variable [test3] equals [undefined] and not [null], because we use the operator [===] and not [==]&quot;</span>);
        }
    <span style="color: blue">&lt;/</span><span style="color: #a31515">script</span><span style="color: blue">&gt;</span></pre>
        <a href="http://11011.net/software/vspaste"></a>

        <p>
          <br /></p>
      </div>
    </div>
  </div>
</div>