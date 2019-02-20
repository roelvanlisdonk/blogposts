---
ID: 3620
post_title: 'Just a reminder: null = null, is not true in T-SQL'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/01/09/just-a-reminder-null-null-is-not-true-in-t-sql/
published: true
post_date: 2014-01-09 16:16:04
---
<p>If you have a nullable column &quot;Description&quot; in one table and a nullable column &quot;Description&quot; in an other table and you join both tables on this column, records with both null in the field &quot;Description&quot; will not match.</p>   <pre class="code"><span style="color: blue">if </span><span style="color: magenta">object_id</span><span style="color: gray">(</span><span style="color: red">'[dbo].[Product1]'</span><span style="color: gray">) is null
</span><span style="color: blue">begin
    create table </span><span style="color: teal">[dbo]</span><span style="color: gray">.</span><span style="color: teal">[Product1]
    </span><span style="color: gray">(
          </span><span style="color: teal">Id </span><span style="color: blue">int </span><span style="color: gray">not null </span><span style="color: blue">identity</span><span style="color: gray">(</span>1<span style="color: gray">,</span>1<span style="color: gray">) </span><span style="color: blue">constraint </span><span style="color: teal">PK_Product1_Id </span><span style="color: blue">primary key</span><span style="color: gray">,
          </span><span style="color: teal">[Description] </span><span style="color: blue">varchar</span><span style="color: gray">(</span><span style="color: magenta">max</span><span style="color: gray">) null
    )
</span><span style="color: blue">end
go

if </span><span style="color: magenta">object_id</span><span style="color: gray">(</span><span style="color: red">'[dbo].[Product2]'</span><span style="color: gray">) is null
</span><span style="color: blue">begin
    create table </span><span style="color: teal">[dbo]</span><span style="color: gray">.</span><span style="color: teal">[Product2]
    </span><span style="color: gray">(
          </span><span style="color: teal">Id </span><span style="color: blue">int </span><span style="color: gray">not null </span><span style="color: blue">identity</span><span style="color: gray">(</span>1<span style="color: gray">,</span>1<span style="color: gray">) </span><span style="color: blue">constraint </span><span style="color: teal">PK_Product2_Id </span><span style="color: blue">primary key</span><span style="color: gray">,
          </span><span style="color: teal">[Description] </span><span style="color: blue">varchar</span><span style="color: gray">(</span><span style="color: magenta">max</span><span style="color: gray">) null
    )
</span><span style="color: blue">end
go

insert into </span><span style="color: teal">Product1 </span><span style="color: blue">values </span><span style="color: gray">(null)
</span><span style="color: blue">insert into </span><span style="color: teal">Product1 </span><span style="color: blue">values </span><span style="color: gray">(</span><span style="color: red">''</span><span style="color: gray">)
</span><span style="color: blue">insert into </span><span style="color: teal">Product1 </span><span style="color: blue">values </span><span style="color: gray">(</span><span style="color: red">'gevuld 1'</span><span style="color: gray">)

</span><span style="color: blue">insert into </span><span style="color: teal">Product2 </span><span style="color: blue">values </span><span style="color: gray">(null)
</span><span style="color: blue">insert into </span><span style="color: teal">Product2 </span><span style="color: blue">values </span><span style="color: gray">(</span><span style="color: red">''</span><span style="color: gray">)
</span><span style="color: blue">insert into </span><span style="color: teal">Product2 </span><span style="color: blue">values </span><span style="color: gray">(</span><span style="color: red">'gevuld 1'</span><span style="color: gray">)


</span><span style="color: blue">select        </span><span style="color: teal">p1</span><span style="color: gray">.*, </span><span style="color: teal">p2</span><span style="color: gray">.*
</span><span style="color: blue">from        </span><span style="color: teal">Product1 p1
</span><span style="color: gray">inner join    </span><span style="color: teal">Product2 p2 </span><span style="color: blue">on </span><span style="color: teal">p1</span><span style="color: gray">.</span><span style="color: teal">[Description] </span><span style="color: gray">= </span><span style="color: teal">p2</span><span style="color: gray">.</span><span style="color: teal">[Description]


</span></pre>

<p>Results in</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/01/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/01/image_thumb.png" width="506" height="232" /></a></p>

<p>&#160;</p>

<p>and you might have expected</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/01/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/01/image_thumb1.png" width="479" height="208" /></a></p>

<p>&#160;</p>

<p>Solution is to use isnull function, like:</p>

<p>&#160;</p>

<pre class="code"><span style="color: blue">select        </span><span style="color: teal">p1</span><span style="color: gray">.*, </span><span style="color: teal">p2</span><span style="color: gray">.*
</span><span style="color: blue">from        </span><span style="color: teal">Product1 p1
</span><span style="color: gray">inner join    </span><span style="color: teal">Product2 p2 </span><span style="color: blue">on </span><span style="color: magenta">isnull</span><span style="color: gray">(</span><span style="color: teal">p1</span><span style="color: gray">.</span><span style="color: teal">[Description]</span><span style="color: gray">, </span><span style="color: red">'Not a value'</span><span style="color: gray">) = </span><span style="color: magenta">isnull</span><span style="color: gray">(</span><span style="color: teal">p2</span><span style="color: gray">.</span><span style="color: teal">[Description]</span><span style="color: gray">, </span><span style="color: red">'Not a value'</span><span style="color: gray">)
</span></pre>