---
ID: 3761
post_title: 'Automatic SQL Server query execution optimization: &quot;get of my lawn&quot;'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/05/13/automatic-sql-server-query-execution-optimization-get-of-my-lawn/
published: true
post_date: 2014-05-13 11:09:49
---
<p>&#160;</p>  <p>I had to write a SQL query, that would return the records where the column &quot;ImportFileName&quot; started with the year &quot;2013&quot;</p>  <p>&#160;</p>  <pre class="code"><span style="color: green">-- Drop temp table if it exists.
</span><span style="color: blue">if </span><span style="color: magenta">object_id</span><span style="color: gray">(</span><span style="color: red">'tempdb..#Import'</span><span style="color: gray">) is not null
</span><span style="color: blue">begin
    drop table </span>#Import
<span style="color: blue">end

</span><span style="color: green">-- Create temp table.
</span><span style="color: blue">create table </span>#Import
<span style="color: gray">(
    </span>Id <span style="color: blue">int </span><span style="color: gray">not null,
    </span>ImportFileName <span style="color: blue">varchar </span><span style="color: gray">(</span>255<span style="color: gray">) not null
)

</span><span style="color: green">-- Seed temp table.
</span><span style="color: blue">insert into </span>#Import <span style="color: gray">(</span>Id<span style="color: gray">, </span>ImportFileName<span style="color: gray">) </span><span style="color: blue">values 
</span><span style="color: gray">(</span>1<span style="color: gray">, </span><span style="color: red">'20130506101010.csv'</span><span style="color: gray">),
(</span>2<span style="color: gray">, </span><span style="color: red">'20130606101010.csv'</span><span style="color: gray">),
(</span>3<span style="color: gray">, </span><span style="color: red">'This_is_an_error_file.csv'</span><span style="color: gray">),
(</span>4<span style="color: gray">, </span><span style="color: red">'20130806101010.csv'</span><span style="color: gray">),
(</span>5<span style="color: gray">, </span><span style="color: red">'20130906101010.csv'</span><span style="color: gray">)

</span><span style="color: green">-- Query the temp table
</span><span style="color: blue">select  </span>Id
        ImportFileName
<span style="color: blue">from    </span>#Import
<span style="color: blue">where   </span><span style="color: magenta">datepart</span><span style="color: gray">(</span><span style="color: magenta">year</span><span style="color: gray">, </span><span style="color: magenta">cast</span><span style="color: gray">(</span><span style="color: magenta">substring</span><span style="color: gray">(</span>ImportFileName<span style="color: gray">, </span>1<span style="color: gray">, </span>8<span style="color: gray">) </span><span style="color: blue">as date</span><span style="color: gray">)) = </span>2013

<span style="color: green">-- Drop temp table.
</span><span style="color: blue">drop table </span>#Import</pre>


<p>This query results in the error:</p>

<pre class="code">Msg 241, Level 16, State 1, Line 19
Conversion failed when converting date and/or time from character string.</pre>
This can be fixed with the SQL Server 2012 and above function: TRY_CONVERT:

<pre class="code"><span style="color: green">-- The fixed query (&gt;= SQL Server 2012)
</span><span style="color: blue">select    </span>Id
        ImportFileName
<span style="color: blue">from    </span>#Import
<span style="color: blue">where    </span><span style="color: magenta">datepart</span><span style="color: gray">(</span><span style="color: magenta">year</span><span style="color: gray">, </span><span style="color: magenta">try_convert</span><span style="color: gray">(</span><span style="color: blue">date</span><span style="color: gray">, </span><span style="color: magenta">substring</span><span style="color: gray">(</span>ImportFileName<span style="color: gray">, </span>1<span style="color: gray">, </span>8<span style="color: gray">))) = </span>2013</pre>


<p>But in SQL Server 2008R2 this function does not exist, so I tried to trick SQL Server by using a subquery that would only return valid records:</p>

<pre class="code"><span style="color: green">-- Query the temp table
</span><span style="color: blue">select  </span>i<span style="color: gray">.</span>Id<span style="color: gray">,
        </span>i<span style="color: gray">.</span>ImportFileName
<span style="color: blue">from    </span><span style="color: gray">(
    </span><span style="color: blue">select    </span>Id<span style="color: gray">,
            </span>ImportFileName
    <span style="color: blue">from    </span>#Import
    <span style="color: blue">where    </span><span style="color: magenta">isdate</span><span style="color: gray">(</span><span style="color: magenta">substring</span><span style="color: gray">(</span>ImportFileName<span style="color: gray">, </span>1<span style="color: gray">, </span>8<span style="color: gray">)) = </span>1
<span style="color: gray">) </span>i
<span style="color: blue">where   </span><span style="color: magenta">datepart</span><span style="color: gray">(</span><span style="color: magenta">year</span><span style="color: gray">, </span><span style="color: magenta">cast</span><span style="color: gray">(</span><span style="color: magenta">substring</span><span style="color: gray">(</span>i<span style="color: gray">.</span>ImportFileName<span style="color: gray">, </span>1<span style="color: gray">, </span>8<span style="color: gray">) </span><span style="color: blue">as date</span><span style="color: gray">)) = </span>2013</pre>

<p>But this resulted in the same error, why????</p>

<p>Well the estimated execution plan tells you why:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/05/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/05/image_thumb.png" width="580" height="172" /></a></p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/05/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/05/image_thumb1.png" width="580" height="220" /></a></p>

<p>&#160;</p>

<p>Effectively SQL Server query optimization will merge the two where statements and convert the query above to something like:</p>

<p>&#160;</p>

<pre class="code"><span style="color: blue">select    </span>Id<span style="color: gray">,
            </span>ImportFileName
    <span style="color: blue">from    </span>#Import
    <span style="color: blue">where    </span><span style="color: magenta">datepart</span><span style="color: gray">(</span><span style="color: magenta">year</span><span style="color: gray">, </span><span style="color: magenta">cast</span><span style="color: gray">(</span><span style="color: magenta">substring</span><span style="color: gray">(</span>ImportFileName<span style="color: gray">, </span>1<span style="color: gray">, </span>8<span style="color: gray">) </span><span style="color: blue">as date</span><span style="color: gray">)) = </span>2013
    <span style="color: gray">and     </span><span style="color: magenta">isdate</span><span style="color: gray">(</span><span style="color: magenta">substring</span><span style="color: gray">(</span>ImportFileName<span style="color: gray">, </span>1<span style="color: gray">, </span>8<span style="color: gray">)) = </span>1</pre>

<p>which will fail.</p>

<p>&#160;</p>

<p>To get around this problem, you could first insert the subquery records in a temp table and then check query the temp table, but in my case I used a case statement:</p>

<pre class="code"><span style="color: green">-- Query the temp table
</span><span style="color: blue">select  </span>i<span style="color: gray">.</span>Id<span style="color: gray">,
        </span>i<span style="color: gray">.</span>ImportFileName
<span style="color: blue">from    </span><span style="color: gray">(
    </span><span style="color: blue">select    </span>Id<span style="color: gray">,
            </span><span style="color: blue">case    when </span><span style="color: magenta">isdate</span><span style="color: gray">(</span><span style="color: magenta">substring</span><span style="color: gray">(</span>ImportFileName<span style="color: gray">, </span>1<span style="color: gray">, </span>8<span style="color: gray">)) = </span>1
                    <span style="color: blue">then    </span>ImportFileName
                    <span style="color: blue">else    </span><span style="color: gray">null
            </span><span style="color: blue">end as </span>ImportFileName
    <span style="color: blue">from    </span>#Import
<span style="color: gray">) </span>i
<span style="color: blue">where   </span><span style="color: magenta">datepart</span><span style="color: gray">(</span><span style="color: magenta">year</span><span style="color: gray">, </span><span style="color: magenta">cast</span><span style="color: gray">(</span><span style="color: magenta">substring</span><span style="color: gray">(</span>i<span style="color: gray">.</span>ImportFileName<span style="color: gray">, </span>1<span style="color: gray">, </span>8<span style="color: gray">) </span><span style="color: blue">as date</span><span style="color: gray">)) = </span>2013</pre>



<p><strong><font size="3">The full script now look like:</font></strong></p>

<pre class="code"><span style="color: green">-- Drop temp table if it exists.
</span><span style="color: blue">if </span><span style="color: magenta">object_id</span><span style="color: gray">(</span><span style="color: red">'tempdb..#Import'</span><span style="color: gray">) is not null
</span><span style="color: blue">begin
    drop table </span>#Import
<span style="color: blue">end

</span><span style="color: green">-- Create temp table.
</span><span style="color: blue">create table </span>#Import
<span style="color: gray">(
    </span>Id <span style="color: blue">int </span><span style="color: gray">not null,
    </span>ImportFileName <span style="color: blue">varchar </span><span style="color: gray">(</span>255<span style="color: gray">) not null
)

</span><span style="color: green">-- Seed temp table.
</span><span style="color: blue">insert into </span>#Import <span style="color: gray">(</span>Id<span style="color: gray">, </span>ImportFileName<span style="color: gray">) </span><span style="color: blue">values 
</span><span style="color: gray">(</span>1<span style="color: gray">, </span><span style="color: red">'20130506101010.csv'</span><span style="color: gray">),
(</span>2<span style="color: gray">, </span><span style="color: red">'20130606101010.csv'</span><span style="color: gray">),
(</span>3<span style="color: gray">, </span><span style="color: red">'This_is_an_error_file.csv'</span><span style="color: gray">),
(</span>4<span style="color: gray">, </span><span style="color: red">'20130806101010.csv'</span><span style="color: gray">),
(</span>5<span style="color: gray">, </span><span style="color: red">'20130906101010.csv'</span><span style="color: gray">)

</span><span style="color: green">-- Query the temp table
</span><span style="color: blue">select  </span>i<span style="color: gray">.</span>Id<span style="color: gray">,
        </span>i<span style="color: gray">.</span>ImportFileName
<span style="color: blue">from    </span><span style="color: gray">(
    </span><span style="color: blue">select    </span>Id<span style="color: gray">,
            </span><span style="color: blue">case    when </span><span style="color: magenta">isdate</span><span style="color: gray">(</span><span style="color: magenta">substring</span><span style="color: gray">(</span>ImportFileName<span style="color: gray">, </span>1<span style="color: gray">, </span>8<span style="color: gray">)) = </span>1
                    <span style="color: blue">then    </span>ImportFileName
                    <span style="color: blue">else    </span><span style="color: gray">null
            </span><span style="color: blue">end as </span>ImportFileName
    <span style="color: blue">from    </span>#Import
<span style="color: gray">) </span>i
<span style="color: blue">where   </span><span style="color: magenta">datepart</span><span style="color: gray">(</span><span style="color: magenta">year</span><span style="color: gray">, </span><span style="color: magenta">cast</span><span style="color: gray">(</span><span style="color: magenta">substring</span><span style="color: gray">(</span>i<span style="color: gray">.</span>ImportFileName<span style="color: gray">, </span>1<span style="color: gray">, </span>8<span style="color: gray">) </span><span style="color: blue">as date</span><span style="color: gray">)) = </span>2013

<span style="color: green">-- Drop temp table.
</span><span style="color: blue">drop table </span>#Import</pre>