---
ID: 1250
post_title: 'How to add a &ldquo;not null&rdquo; column to a table using t-sql alter table statement in Microsoft SQL Server'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/04/20/how-to-add-a-not-null-column-to-a-table-using-t-sql-alter-table-statement-in-microsoft-sql-server/
published: true
post_date: 2010-04-20 09:26:05
---
<p>There are two options for adding a “not null” column to a table using t-sql alter table statement in Microsoft SQL Server.</p>  <ul>   <li>Add a default to the new column, which sets the value of existing records to a not null value </li>    <li>Add the column as a “null” column, set the value of existing records then change the column to a “not null” column </li> </ul>  <p>Both have there pros and cons, using a default may impact performance but is less code. using the other approach might be better for production performance but is more code and the new column must be supplied by inserts.</p>  <p>&#160;</p>  <p>&#160;</p>  <p><strong>Using a default</strong></p>  <p>&#160;</p>  <pre class="code"><span style="color: blue">use <span style="color: #000000">MyDatabase</span></span>
<span style="color: blue">go </span><span style="color: green">-- Add the column &quot;MyColumn1&quot; to table &quot;MyTable&quot; as &quot;NOT NULL&quot;
</span><span style="color: blue">if </span><span style="color: gray">exists (</span><span style="color: blue">select </span>1 <span style="color: blue">from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">objects </span><span style="color: blue">where </span>name <span style="color: gray">= </span><span style="color: red">'MyTable' </span><span style="color: gray">and </span><span style="color: blue">type </span><span style="color: gray">= </span><span style="color: red">'U'</span><span style="color: gray">) 
</span><span style="color: blue">begin 
 if </span><span style="color: gray">not exists (</span><span style="color: blue">select </span>1 <span style="color: blue">from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">columns </span><span style="color: blue">where </span>name <span style="color: gray">= </span><span style="color: red">'MyColumn1' </span><span style="color: blue">and Object_ID </span>= <span style="color: blue">Object_ID</span>(<span style="color: #a31515">'MyTable'</span>)<span style="color: gray">) 
</span><span style="color: blue"> begin 
   alter table </span>MyTable <span style="color: blue">with nocheck add </span>MyColumn1 <span style="color: blue">int </span><span style="color: gray">not null </span><span style="color: blue">default</span><span style="color: gray">(</span>0<span style="color: gray">)&#160; </span><span style="color: blue"> end<br /></span><span style="color: blue">end go</span></pre>

<p>&#160;</p>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>Adding as “null”, then change to “not null”</strong></p>

<pre class="code"><p><span style="color: blue">use <span style="color: #000000">MyDatabase</span></span>
<span style="color: blue">go 
</span><span style="color: green">-- Add the column &quot;MyColumn2&quot; to table &quot;MyTable&quot; as &quot;NULL&quot;
</span><span style="color: blue">if </span><span style="color: gray">exists (</span><span style="color: blue">select </span>1 <span style="color: blue">from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">objects </span><span style="color: blue">where Object_ID = Object_ID('MyTable')</span><span style="color: gray">)
</span><span style="color: blue">begin if </span><span style="color: gray">not exists (</span><span style="color: blue">select </span>1 <span style="color: blue">from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">columns </span><span style="color: blue">where </span>name <span style="color: gray">= </span><span style="color: red">'MyColumn2' </span><span style="color: blue">and Object_ID </span>= <span style="color: blue">Object_ID</span>(<span style="color: #a31515">'MyTable'</span>)<span style="color: gray">)
</span><span style="color: blue"> begin <br />   alter table </span>MyTable <span style="color: blue">with nocheck add </span>MyColumn2 <span style="color: blue">int </span><span style="color: gray">null
</span><span style="color: blue"> end
end go </span></p><p><span style="color: blue"></span><span style="color: green">-- Change value of existing records <br /></span><span style="color: blue">if </span><span style="color: gray">exists (</span><span style="color: blue">select </span>1 <span style="color: blue">from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">objects </span><span style="color: blue">where Object_ID = Object_ID('MyTable')</span><span style="color: gray">) <br /></span><span style="color: blue">begin <br />  if </span><span style="color: gray">exists (</span><span style="color: blue">select </span>1 <span style="color: blue">from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">columns </span><span style="color: blue">where </span>name <span style="color: gray">= </span><span style="color: red">'MyColumn2' </span><span style="color: blue">and Object_ID </span>= <span style="color: blue">Object_ID</span>(<span style="color: #a31515">'MyTable'</span>) and is_nullable = 1<span style="color: gray">) <br />  </span><span style="color: blue">begin <br />    </span><span style="color: blue">update </span>MyTable <span style="color: blue">set </span>MyColumn2 <span style="color: gray">= </span>0<br />  <span style="color: blue">end<br />end<br />go</span></p><p><span style="color: blue"><br /></span><span style="color: green"><br /><br />-- Change &quot;NULL&quot; column to &quot;NOT NULL&quot; column<br /></span><span style="color: blue">if </span><span style="color: gray">exists (</span><span style="color: blue">select </span>1 <span style="color: blue">from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">objects </span><span style="color: blue">where Object_ID = Object_ID('MyTable')</span><span style="color: gray">)<br /></span><span style="color: blue">begin<br />  if </span><span style="color: gray">exists (</span><span style="color: blue">select </span>1 <span style="color: blue">from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">columns </span><span style="color: blue">where </span>name <span style="color: gray">= </span><span style="color: red">'MyColumn2' </span><span style="color: blue">and Object_ID </span>= <span style="color: blue">Object_ID</span>(<span style="color: #a31515">'MyTable'</span>) and is_nullable = 1<span style="color: gray">)<br />  </span><span style="color: blue">begin<br /></span><span style="color: blue">    alter table </span>MyTable <span style="color: blue">alter column </span>MyColumn2 <span style="color: blue">int </span><span style="color: gray">not null<br /></span><span style="color: blue">  end<br />end<br />go</span></p></pre>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>Note</strong></p>

<p>If you’re table has a schema name use <span style="color: blue">Object_ID</span>(<span style="color: #a31515">'MySchema.MyTable'</span>)</p>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>MSDN documentation</strong></p>

<p>NULL / NOT NULL: Specifies whether the column can accept null values. Columns that do not allow null values can be added with ALTER TABLE only if they have a default specified. A new column added to a table must either allow null values, or the column must be specified with a default value.</p>

<p><a title="http://msdn.microsoft.com/en-us/library/aa275462(SQL.80).aspx" href="http://msdn.microsoft.com/en-us/library/aa275462(SQL.80).aspx">http://msdn.microsoft.com/en-us/library/aa275462(SQL.80).aspx</a></p>