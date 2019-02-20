---
ID: 1824
post_title: >
  Using an T-SQL update statement with a
  @COUTNER variable to provide consecutive
  numbers in a column
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/11/10/using-an-t-sql-update-statement-with-a-coutner-variable-to-provide-consecutive-numbers-in-a-column/
published: true
post_date: 2010-11-10 11:53:58
---
<p>If you have a table in a Microsoft SQL Server database with an integer column that contains rows and you want to update the existing rows to&#160; contain consecutive numbers, you can use the following T-SQL query:</p> <a href="http://11011.net/software/vspaste"></a>  <pre class="code"><span style="color: blue">declare </span>@COUNTER <span style="color: blue">as int
set </span>@COUNTER <span style="color: gray">= </span>0 <span style="color: green">-- First number will be [1] 

-- Update the [Number] column, so it contains consecutive numbers
</span><span style="color: blue">update        </span>[TestTable]
<span style="color: blue">set            </span>[Number] <span style="color: gray">= </span>@COUNTER<span style="color: gray">, </span>@COUNTER <span style="color: gray">= </span>@COUNTER <span style="color: gray">+ </span>1</pre>
<a href="http://11011.net/software/vspaste"></a>