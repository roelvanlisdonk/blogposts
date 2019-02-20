---
ID: 2489
post_title: >
  How to create a stored procedure with
  T-SQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/02/07/how-to-create-a-stored-procedure-with-t-sql/
published: true
post_date: 2012-02-07 08:46:21
---
<p>Well for ages, I created mine stored procedures like:</p>  <pre class="code"><span style="color: blue">if </span><span style="color: gray">exists (</span><span style="color: blue">select </span>1 <span style="color: blue">from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">objects </span><span style="color: blue">where </span>name <span style="color: gray">= </span><span style="color: red">'GetSales' </span><span style="color: gray">and </span><span style="color: blue">type </span><span style="color: gray">= </span><span style="color: red">'p'</span><span style="color: gray">)
</span><span style="color: blue">begin
    drop procedure </span>[Reporting]<span style="color: gray">.</span>[GetSales]
<span style="color: blue">end
go

create procedure </span>[Reporting]<span style="color: gray">.</span>[GetSales]
    @parameter1 <span style="color: blue">int</span><span style="color: gray">,
    </span>@parameter2 <span style="color: blue">int
as
begin
    select </span>@parameter1<span style="color: gray">, </span>@parameter2    
<span style="color: blue">end
go
</span></pre>

<p>, but there is a slightly shorter notation:</p>

<pre class="code"><span style="color: blue">if </span><span style="color: magenta">object_id</span><span style="color: gray">(</span><span style="color: red">'[Reporting].[GetSales]'</span><span style="color: gray">) is not null
</span><span style="color: blue">begin
    drop procedure </span>[Reporting]<span style="color: gray">.</span>[GetSales]
<span style="color: blue">end
go

create procedure </span>[Reporting]<span style="color: gray">.</span>[GetSales]
    @parameter1 <span style="color: blue">int</span><span style="color: gray">,
    </span>@parameter2 <span style="color: blue">int
as
begin
    select </span>@parameter1<span style="color: gray">, </span>@parameter2    
<span style="color: blue">end
go</span></pre>


<p>&#160;</p>

<p>&#160;</p>

<p>You’re never to old to learn <img style="border-bottom-style: none; border-left-style: none; border-top-style: none; border-right-style: none" class="wlEmoticon wlEmoticon-winkingsmile" alt="Winking smile" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/02/wlEmoticon-winkingsmile.png" />.</p>