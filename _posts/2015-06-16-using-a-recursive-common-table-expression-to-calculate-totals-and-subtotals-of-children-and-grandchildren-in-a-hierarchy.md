---
ID: 4391
post_title: >
  Using a recursive common table
  expression, to calculate totals and
  subtotals of children and grandchildren
  in a hierarchy
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/06/16/using-a-recursive-common-table-expression-to-calculate-totals-and-subtotals-of-children-and-grandchildren-in-a-hierarchy/
published: true
post_date: 2015-06-16 21:43:43
---
<p>In SQL Server a common table expression can be used to calculate totals / subtotals of a table containing hierarchical data:</p>  <p>&#160;</p>  <pre class="code"><span style="color: green">-- Create test data:
</span><span style="color: blue">if </span><span style="color: magenta">object_id</span><span style="color: gray">(</span><span style="color: red">'tempdb..#Hierarchy'</span><span style="color: gray">) is not null
</span><span style="color: blue">begin
    drop table </span>#Hierarchy
<span style="color: blue">end

create table </span>#Hierarchy <span style="color: gray">(
    </span>Id <span style="color: blue">int </span><span style="color: gray">not null,
    </span>ParentId <span style="color: blue">int </span><span style="color: gray">null,
    </span>Amount <span style="color: blue">int </span><span style="color: gray">not null
)

</span><span style="color: blue">insert into </span>#Hierarchy <span style="color: gray">(</span>Id<span style="color: gray">, </span>ParentId<span style="color: gray">, </span>Amount<span style="color: gray">) </span><span style="color: blue">values
    </span><span style="color: gray">(</span>1<span style="color: gray">, null, </span>100<span style="color: gray">)
,    (</span>2<span style="color: gray">, </span>1<span style="color: gray">, </span>100<span style="color: gray">)
,   (</span>3<span style="color: gray">, </span>1<span style="color: gray">, </span>100<span style="color: gray">)
,   (</span>4<span style="color: gray">, </span>1<span style="color: gray">, </span>100<span style="color: gray">)
,   (</span>5<span style="color: gray">, </span>4<span style="color: gray">, </span>100<span style="color: gray">)
,   (</span>6<span style="color: gray">, </span>4<span style="color: gray">, </span>100<span style="color: gray">)
,   (</span>7<span style="color: gray">, </span>4<span style="color: gray">, </span>100<span style="color: gray">)
,   (</span>8<span style="color: gray">, </span>7<span style="color: gray">, </span>100<span style="color: gray">)

;</span><span style="color: blue">with </span>CTE <span style="color: gray">(</span>ParentId<span style="color: gray">, </span>Id<span style="color: gray">, </span>Amount<span style="color: gray">, </span>IsParent<span style="color: gray">)
</span><span style="color: blue">as
</span><span style="color: gray">(
    </span><span style="color: green">-- Add all records as &quot;anchor&quot;, because foreach record we are going to calculate the total amount.
    </span><span style="color: blue">select    </span>h<span style="color: gray">.</span>ParentId
    <span style="color: gray">,        </span>h<span style="color: gray">.</span>Id
    <span style="color: gray">,        </span>h<span style="color: gray">.</span>Amount
    <span style="color: gray">,        </span>0 <span style="color: blue">as </span>IsParent
    <span style="color: blue">from    </span>#Hierarchy h
    <span style="color: blue">union </span><span style="color: gray">all
    </span><span style="color: green">-- Recursively add parent records until root parent foreach record in &quot;anchor&quot;.
    </span><span style="color: blue">select    </span>h<span style="color: gray">.</span>ParentId
    <span style="color: gray">,        </span>h<span style="color: gray">.</span>Id
    <span style="color: gray">,        </span>h<span style="color: gray">.</span>Amount
    <span style="color: gray">,        </span>1 <span style="color: blue">as </span>IsParent
    <span style="color: blue">from    </span>CTE c
    <span style="color: gray">join    </span>#Hierarchy h <span style="color: blue">on </span>c<span style="color: gray">.</span>ParentId <span style="color: gray">= </span>h<span style="color: gray">.</span>Id
<span style="color: gray">)

</span><span style="color: blue">select        </span>c1<span style="color: gray">.</span>Id
<span style="color: gray">,            </span>c1<span style="color: gray">.</span>ParentId
<span style="color: gray">,            </span><span style="color: magenta">sum</span><span style="color: gray">(</span>c1<span style="color: gray">.</span>Amount<span style="color: gray">) </span><span style="color: blue">as </span>TotalAmount
<span style="color: gray">,            </span><span style="color: blue">case when </span><span style="color: magenta">sum</span><span style="color: gray">(</span>c1<span style="color: gray">.</span>IsParent<span style="color: gray">) &gt; </span>0 <span style="color: blue">then </span>1 <span style="color: blue">else </span>0 <span style="color: blue">end as </span>IsParent
<span style="color: blue">from        </span>CTE c1
<span style="color: blue">group by    </span>c1<span style="color: gray">.</span>Id<span style="color: gray">, </span>c1<span style="color: gray">.</span>ParentId</pre>


<pre class="code"><span style="color: green"></span></pre>

<p><strong>Result</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/06/image6.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/06/image_thumb6.png" width="378" height="295" /></a></p>