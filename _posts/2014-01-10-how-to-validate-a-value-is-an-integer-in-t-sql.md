---
ID: 3642
post_title: >
  How to validate a value can be cast to
  an integer in T-SQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/01/10/how-to-validate-a-value-is-an-integer-in-t-sql/
published: true
post_date: 2014-01-10 10:11:59
---
<p>Validating if a value is an integer can be done by using TRY_CAST in SQL Server 2012 or a combination of ISNUMERIC and cast to float in &lt;= SQL Server 2008.</p>  <pre class="code"><span style="background: white; color: blue">declare </span><span style="background: white; color: black">@value </span><span style="background: white; color: blue">as varchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">255</span><span style="background: white; color: gray">) = </span><span style="background: white; color: red">'1.6'

</span><span style="background: white; color: green">-- SQL Server 2008
</span><span style="background: white; color: blue">select case        when </span><span style="background: white; color: magenta">isnumeric</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">@value</span><span style="background: white; color: gray">) = </span><span style="background: white; color: black">1
                </span><span style="background: white; color: blue">then </span><span style="background: white; color: red">'Cast succeeded, value is: ' </span><span style="background: white; color: gray">+ </span><span style="background: white; color: magenta">cast</span><span style="background: white; color: gray">(</span><span style="background: white; color: magenta">cast</span><span style="background: white; color: gray">(</span><span style="background: white; color: magenta">cast</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">@value </span><span style="background: white; color: blue">as float</span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">as int</span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">as varchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">255</span><span style="background: white; color: gray">))
                </span><span style="background: white; color: blue">else </span><span style="background: white; color: red">'Cast failed.'
       </span><span style="background: white; color: blue">end as    </span><span style="background: white; color: black">Result

</span><span style="background: white; color: green">-- SQL Server 2012
</span><span style="background: white; color: blue">select    case    when </span><span style="background: white; color: black">try_cast</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">@value </span><span style="background: white; color: blue">as float</span><span style="background: white; color: gray">) is not null 
                </span><span style="background: white; color: blue">then </span><span style="background: white; color: red">'Cast succeeded, value is: ' </span><span style="background: white; color: gray">+ </span><span style="background: white; color: magenta">cast</span><span style="background: white; color: gray">(</span><span style="background: white; color: magenta">cast</span><span style="background: white; color: gray">(</span><span style="background: white; color: magenta">cast</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">@value </span><span style="background: white; color: blue">as float</span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">as int</span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">as varchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">255</span><span style="background: white; color: gray">))
                </span><span style="background: white; color: blue">else </span><span style="background: white; color: red">'Cast failed.'
        </span><span style="background: white; color: blue">end as    </span><span style="background: white; color: black">Result</span></pre>


<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/01/image3.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/01/image_thumb3.png" width="286" height="337" /></a></p>

<p>&#160;</p>

<p>If you use try_cast(@value as int) the cast will fail on a float ‘1.6’, like:</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/01/image4.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/01/image_thumb4.png" width="580" height="239" /></a></p>