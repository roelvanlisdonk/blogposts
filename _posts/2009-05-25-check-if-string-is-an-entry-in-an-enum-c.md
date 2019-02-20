---
ID: 473
post_title: 'Check if string is an entry in an enum C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/25/check-if-string-is-an-entry-in-an-enum-c/
published: true
post_date: 2009-05-25 12:55:26
---
<div class="padten">   <div class="ms-inputuserfield padfive seventyp">     <div>       <div class="ExternalClass730205FE59C1460699797176E6C24ABC">         <p>If you want to check if a string is defined in an enum, with C#, use the Enum.IsDefined function</p>          <pre class="code"><span style="color: blue">       public enum </span><span style="color: #2b91af">CarTypes
       </span>{
           Alfa,
           Audi,
           BMW
       }
       <span style="color: blue">public void </span>TestEnum()
       {
           <span style="color: blue">if </span>(<span style="color: #2b91af">Enum</span>.IsDefined(<span style="color: blue">typeof</span>(<span style="color: #2b91af">CarTypes</span>), <span style="color: #a31515">&quot;Audi&quot;</span>))
           {
               <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: #a31515">&quot;Yes the string Audi is an entry in the enum CarTypes&quot;
           </span>}
       }</pre>
      </div>
    </div>
  </div>
</div>