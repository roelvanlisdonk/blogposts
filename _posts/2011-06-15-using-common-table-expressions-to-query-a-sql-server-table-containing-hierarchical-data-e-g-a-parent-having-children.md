---
ID: 2093
post_title: >
  Using Common Table Expressions to query
  a SQL Server table containing
  hierarchical data (e.g. a parent having
  children)
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/06/15/using-common-table-expressions-to-query-a-sql-server-table-containing-hierarchical-data-e-g-a-parent-having-children/
published: true
post_date: 2011-06-15 09:45:04
---
<p>If you have a table containing hierarchical data (e.g. a parent having children) and you want to show all the children and grand children for a person you can use a &quot;Common Table Expression&quot; in Microsoft SQL Server 2008.</p>  <p>&#160;</p>  <p><strong>Table Person</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/06/image.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/06/image_thumb.png" width="406" height="172" /></a></p>  <p>&#160;</p>  <p><strong>Table Person Data</strong></p>  <pre class="code"><span style="color: blue">truncate table </span>person
<span style="color: blue">insert into </span>person <span style="color: gray">(</span>Id<span style="color: gray">, </span>Name<span style="color: gray">, </span>Birthday<span style="color: gray">, </span>ParentId<span style="color: gray">) </span><span style="color: blue">values </span><span style="color: gray">(</span>1<span style="color: gray">, </span><span style="color: red">'John Do'</span><span style="color: gray">, </span><span style="color: red">'1950-6-1'</span><span style="color: gray">, null)
</span><span style="color: blue">insert into </span>person <span style="color: gray">(</span>Id<span style="color: gray">, </span>Name<span style="color: gray">, </span>Birthday<span style="color: gray">, </span>ParentId<span style="color: gray">) </span><span style="color: blue">values </span><span style="color: gray">(</span>2<span style="color: gray">, </span><span style="color: red">'Carl Do'</span><span style="color: gray">, </span><span style="color: red">'1980-3-5'</span><span style="color: gray">, </span>1<span style="color: gray">)
</span><span style="color: blue">insert into </span>person <span style="color: gray">(</span>Id<span style="color: gray">, </span>Name<span style="color: gray">, </span>Birthday<span style="color: gray">, </span>ParentId<span style="color: gray">) </span><span style="color: blue">values </span><span style="color: gray">(</span>3<span style="color: gray">, </span><span style="color: red">'Michael Do'</span><span style="color: gray">, </span><span style="color: red">'2010-12-12'</span><span style="color: gray">, </span>2<span style="color: gray">)
</span><span style="color: blue">insert into </span>person <span style="color: gray">(</span>Id<span style="color: gray">, </span>Name<span style="color: gray">, </span>Birthday<span style="color: gray">, </span>ParentId<span style="color: gray">) </span><span style="color: blue">values </span><span style="color: gray">(</span>4<span style="color: gray">, </span><span style="color: red">'Tonny Jackson'</span><span style="color: gray">, </span><span style="color: red">'1915-3-3'</span><span style="color: gray">, null)
</span><span style="color: blue">insert into </span>person <span style="color: gray">(</span>Id<span style="color: gray">, </span>Name<span style="color: gray">, </span>Birthday<span style="color: gray">, </span>ParentId<span style="color: gray">) </span><span style="color: blue">values </span><span style="color: gray">(</span>5<span style="color: gray">, </span><span style="color: red">'Bo Jackson'</span><span style="color: gray">, </span><span style="color: red">'1945-7-7'</span><span style="color: gray">, </span>4<span style="color: gray">)
</span><span style="color: blue">insert into </span>person <span style="color: gray">(</span>Id<span style="color: gray">, </span>Name<span style="color: gray">, </span>Birthday<span style="color: gray">, </span>ParentId<span style="color: gray">) </span><span style="color: blue">values </span><span style="color: gray">(</span>6<span style="color: gray">, </span><span style="color: red">'Harry Jackson'</span><span style="color: gray">, </span><span style="color: red">'1981-4-4'</span><span style="color: gray">, </span>5<span style="color: gray">)
</span><span style="color: blue">insert into </span>person <span style="color: gray">(</span>Id<span style="color: gray">, </span>Name<span style="color: gray">, </span>Birthday<span style="color: gray">, </span>ParentId<span style="color: gray">) </span><span style="color: blue">values </span><span style="color: gray">(</span>7<span style="color: gray">, </span><span style="color: red">'Bart Jackson'</span><span style="color: gray">, </span><span style="color: red">'2009-12-11'</span><span style="color: gray">, </span>6<span style="color: gray">)</span></pre>


<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/06/image1.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/06/image_thumb1.png" width="382" height="226" /></a></p>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>Returning a person with all it’s children and grandchildren</strong></p>


<pre class="code"><span style="color: blue">declare </span>@PersonId <span style="color: blue">int
set </span>@PersonId <span style="color: gray">= </span>4

<span style="color: green">-- Define the &quot;Common Table Expression&quot; with name &quot;person_cte&quot;
</span><span style="color: gray">; </span><span style="color: blue">with </span>person_cte <span style="color: blue">as </span><span style="color: gray">(
 
 </span><span style="color: green">-- Select all the direct children of the given person
 </span><span style="color: blue">select        </span>p2<span style="color: gray">.</span>Id<span style="color: gray">,
             </span>p2<span style="color: gray">.</span>Name<span style="color: gray">,
            </span>p2<span style="color: gray">.</span>Birthday<span style="color: gray">,
            </span>p2<span style="color: gray">.</span>ParentId
 <span style="color: blue">from        </span>person p1
 <span style="color: gray">inner join </span>person p2 <span style="color: blue">on </span>p2<span style="color: gray">.</span>ParentId <span style="color: gray">= </span>p1<span style="color: gray">.</span>Id
 <span style="color: blue">where        </span>p1<span style="color: gray">.</span>Id <span style="color: gray">= </span>@PersonId 

 <span style="color: blue">union </span><span style="color: gray">all

 </span><span style="color: green">-- Add grandchildren's, by recursively calling this &quot;Common Table Expression&quot;
 </span><span style="color: blue">select        </span>p1<span style="color: gray">.</span>Id<span style="color: gray">,
            </span>p1<span style="color: gray">.</span>Name<span style="color: gray">,
            </span>p1<span style="color: gray">.</span>Birthday<span style="color: gray">,
            </span>p1<span style="color: gray">.</span>ParentId
 <span style="color: blue">from        </span>person_cte p2
 <span style="color: gray">inner join </span>person p1 <span style="color: blue">on </span>p1<span style="color: gray">.</span>ParentId <span style="color: gray">= </span>p2<span style="color: gray">.</span>Id
 
<span style="color: gray">) 
</span><span style="color: blue">select
    </span>Id<span style="color: gray">,
    </span>Name<span style="color: gray">,
    </span>Birthday<span style="color: gray">,
    </span>ParentId
<span style="color: blue">from </span>person_cte

<span style="color: blue">union </span><span style="color: gray">all

</span><span style="color: green">-- Add the given person to the result
</span><span style="color: blue">select
    </span>Id<span style="color: gray">,
    </span>Name<span style="color: gray">,
    </span>Birthday<span style="color: gray">,
    </span>ParentId
<span style="color: blue">from </span>person
<span style="color: blue">where </span>Id <span style="color: gray">= </span>@PersonId
<span style="color: blue">order by </span>Birthday</pre>


<p><strong>Result</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/06/image2.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/06/image_thumb2.png" width="429" height="151" /></a></p>

<p>&#160;</p>

<p><strong>Background information:</strong></p>

<p>Using Common Table Expressions: <a href="http://msdn.microsoft.com/en-us/library/ms190766.aspx">http://msdn.microsoft.com/en-us/library/ms190766.aspx</a></p>

<p>Recursive Queries Using Common Table Expressions: <a title="http://msdn.microsoft.com/en-us/library/ms186243.aspx" href="http://msdn.microsoft.com/en-us/library/ms186243.aspx">http://msdn.microsoft.com/en-us/library/ms186243.aspx</a></p>