---
ID: 2765
post_title: >
  How to correctly use select top 1 inside
  a inner join of an update statement in
  T-SQL.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/07/11/how-to-correctly-use-select-top-1-inside-a-inner-join-of-an-update-statement-in-t-sql/
published: true
post_date: 2012-07-11 09:17:08
---
<p>And the answer is: don’t use select top 1, instead use the row_number() function and the OVER clause.</p>  <p>Lets assume we have a table structure like:</p>  <p>&#160;</p>  <p>&#160;</p>  <p><strong>Table [Observation]</strong></p>  <p>Multiple observations during a TimeSpan on 1 barcode are collected into 1 [Observation] record.</p>   <p>&#160;</p>  <p><strong>     <pre class="code"><span style="color: blue">if </span><span style="color: magenta">object_id</span><span style="color: gray">(</span><span style="color: red">'[dbo].[Observation]'</span><span style="color: gray">) is null
</span><span style="color: blue">begin
  create table </span>[dbo]<span style="color: gray">.</span>[Observation]
  <span style="color: gray">(
      </span>[Id]                <span style="color: blue">int </span><span style="color: gray">not null </span><span style="color: blue">identity</span><span style="color: gray">(</span>1<span style="color: gray">,</span>1<span style="color: gray">)  </span><span style="color: blue">constraint </span>PK_Observation_Id <span style="color: blue">primary key</span><span style="color: gray">,
      </span>[Barcode]            <span style="color: blue">varchar</span><span style="color: gray">(</span><span style="color: magenta">max</span><span style="color: gray">) not null,
      </span>[Postcode]        <span style="color: blue">varchar</span><span style="color: gray">(</span><span style="color: magenta">max</span><span style="color: gray">) not null,
      </span>[Date]            <span style="color: blue">date </span><span style="color: gray">not null,
      </span>[Count]            <span style="color: blue">int </span><span style="color: gray">not null,
      </span>[TimeSpanId]        <span style="color: blue">int </span><span style="color: gray">not null </span><span style="color: blue">constraint </span>FK_Observation_TimeSpanId <span style="color: blue">foreign key references </span>TimeSpan<span style="color: gray">(</span>Id<span style="color: gray">)
  )
</span><span style="color: blue">end
go

if </span><span style="color: gray">not exists(</span><span style="color: blue">select top </span>1 1 <span style="color: blue">from </span>[Observation]<span style="color: gray">)
</span><span style="color: blue">begin
    insert into </span>[dbo]<span style="color: gray">.</span>Observation<span style="color: gray">(</span>[Barcode]<span style="color: gray">,</span>[Postcode]<span style="color: gray">,</span>[Date]<span style="color: gray">,</span>[Count]<span style="color: gray">,</span>[TimeSpanId]<span style="color: gray">) </span><span style="color: blue">values </span><span style="color: gray">(</span><span style="color: red">'NN10000'</span><span style="color: gray">,</span><span style="color: red">'4000AA'</span><span style="color: gray">,</span><span style="color: red">'2012-06-18'</span><span style="color: gray">,</span>1<span style="color: gray">,</span>1<span style="color: gray">)
    </span><span style="color: blue">insert into </span>[dbo]<span style="color: gray">.</span>Observation<span style="color: gray">(</span>[Barcode]<span style="color: gray">,</span>[Postcode]<span style="color: gray">,</span>[Date]<span style="color: gray">,</span>[Count]<span style="color: gray">,</span>[TimeSpanId]<span style="color: gray">) </span><span style="color: blue">values </span><span style="color: gray">(</span><span style="color: red">'NN10001'</span><span style="color: gray">,</span><span style="color: red">'4000AA'</span><span style="color: gray">,</span><span style="color: red">'2012-07-02'</span><span style="color: gray">,</span>1<span style="color: gray">,</span>1<span style="color: gray">)
    </span><span style="color: blue">insert into </span>[dbo]<span style="color: gray">.</span>Observation<span style="color: gray">(</span>[Barcode]<span style="color: gray">,</span>[Postcode]<span style="color: gray">,</span>[Date]<span style="color: gray">,</span>[Count]<span style="color: gray">,</span>[TimeSpanId]<span style="color: gray">) </span><span style="color: blue">values </span><span style="color: gray">(</span><span style="color: red">'NN20000'</span><span style="color: gray">,</span><span style="color: red">'4000AA'</span><span style="color: gray">,</span><span style="color: red">'2012-05-29'</span><span style="color: gray">,</span>2<span style="color: gray">,</span>2<span style="color: gray">)
    </span><span style="color: blue">insert into </span>[dbo]<span style="color: gray">.</span>Observation<span style="color: gray">(</span>[Barcode]<span style="color: gray">,</span>[Postcode]<span style="color: gray">,</span>[Date]<span style="color: gray">,</span>[Count]<span style="color: gray">,</span>[TimeSpanId]<span style="color: gray">) </span><span style="color: blue">values </span><span style="color: gray">(</span><span style="color: red">'NN30000'</span><span style="color: gray">,</span><span style="color: red">'4000AA'</span><span style="color: gray">,</span><span style="color: red">'2012-06-18'</span><span style="color: gray">,</span>2<span style="color: gray">,</span>3<span style="color: gray">)
</span><span style="color: blue">end
</span></pre>
    Table [TimeSpan]</strong></p>

<p>The table TimeSpan contains timespans of 2 hours.</p>

<pre class="code"><span style="color: blue">if </span><span style="color: magenta">object_id</span><span style="color: gray">(</span><span style="color: red">'[dbo].[TimeSpan]'</span><span style="color: gray">) is null
</span><span style="color: blue">begin
  create table </span>[dbo]<span style="color: gray">.</span>[TimeSpan]
  <span style="color: gray">(
      </span>[Id]                <span style="color: blue">int </span><span style="color: gray">not null </span><span style="color: blue">identity</span><span style="color: gray">(</span>1<span style="color: gray">,</span>1<span style="color: gray">)  </span><span style="color: blue">constraint </span>PK_TimeSpan_Id <span style="color: blue">primary key</span><span style="color: gray">,
      </span>[Name]            <span style="color: blue">varchar</span><span style="color: gray">(</span><span style="color: magenta">max</span><span style="color: gray">),
      </span>[Start]            <span style="color: blue">time</span><span style="color: gray">(</span>7<span style="color: gray">),
      </span>[End]                <span style="color: blue">time</span><span style="color: gray">(</span>7<span style="color: gray">),
      </span>[IsMostImportant] <span style="color: blue">int </span><span style="color: gray">not null </span><span style="color: blue">default</span><span style="color: gray">(</span>0<span style="color: gray">)
  )
</span><span style="color: blue">end
go

if </span><span style="color: gray">not exists(</span><span style="color: blue">select top </span>1 1 <span style="color: blue">from </span>[TimeSpan]<span style="color: gray">)
</span><span style="color: blue">begin
    insert into </span>[dbo]<span style="color: gray">.</span>[TimeSpan]<span style="color: gray">(</span>[Name]<span style="color: gray">,</span>[Start]<span style="color: gray">,</span>[End]<span style="color: gray">,</span>[IsMostImportant]<span style="color: gray">) </span><span style="color: blue">values </span><span style="color: gray">(</span><span style="color: red">'07:00 - 09:00'</span><span style="color: gray">,</span><span style="color: red">'07:00:00'</span><span style="color: gray">,</span><span style="color: red">'09:00:00'</span><span style="color: gray">,</span>0<span style="color: gray">)
    </span><span style="color: blue">insert into </span>[dbo]<span style="color: gray">.</span>[TimeSpan]<span style="color: gray">(</span>[Name]<span style="color: gray">,</span>[Start]<span style="color: gray">,</span>[End]<span style="color: gray">,</span>[IsMostImportant]<span style="color: gray">) </span><span style="color: blue">values </span><span style="color: gray">(</span><span style="color: red">'10:00 - 12:00'</span><span style="color: gray">,</span><span style="color: red">'10:00:00'</span><span style="color: gray">,</span><span style="color: red">'12:00:00'</span><span style="color: gray">,</span>0<span style="color: gray">)           
    </span><span style="color: blue">insert into </span>[dbo]<span style="color: gray">.</span>[TimeSpan]<span style="color: gray">(</span>[Name]<span style="color: gray">,</span>[Start]<span style="color: gray">,</span>[End]<span style="color: gray">,</span>[IsMostImportant]<span style="color: gray">) </span><span style="color: blue">values </span><span style="color: gray">(</span><span style="color: red">'13:00 - 15:00'</span><span style="color: gray">,</span><span style="color: red">'13:00:00'</span><span style="color: gray">,</span><span style="color: red">'15:00:00'</span><span style="color: gray">,</span>0<span style="color: gray">)
</span><span style="color: blue">end

</span></pre>


<p><strong>The most important TimeSpan</strong></p>

<p>The first TimeSpan with the most- and youngest observations.</p>

<p>&#160;</p>

<p><strong>Update Query</strong></p>

<p>The column [IsMostImportant] can be updated by using the following query:</p>

<pre class="code"><span style="color: blue">declare    </span>@DateNow <span style="color: blue">date
set </span>@DateNow <span style="color: gray">= </span><span style="color: red">'2012-07-12'
</span><span style="color: blue">set nocount on                                </span><span style="color: green">-- SET NOCOUNT ON, added to prevent extra result sets from interfering with SELECT statements.
</span><span style="color: blue">set datefirst </span>1                               <span style="color: green">-- Monday is first day of the week.

</span><span style="color: magenta">update </span>[TimeSpan]
<span style="color: blue">set </span>[IsMostImportant] <span style="color: gray">= </span>1
<span style="color: blue">from </span>[TimeSpan] ts
<span style="color: gray">inner join
(
    </span><span style="color: blue">select
        </span>ob3<span style="color: gray">.</span>[RowNumber]<span style="color: gray">,
        </span>ob3<span style="color: gray">.</span>[TimeSpanId]
    <span style="color: blue">from
    </span><span style="color: gray">(
        </span><span style="color: blue">select
            </span><span style="color: magenta">row_number</span><span style="color: gray">() </span><span style="color: blue">over</span><span style="color: gray">(</span><span style="color: blue">partition by </span>ob2<span style="color: gray">.</span>[Postcode] <span style="color: blue">order by </span>ob2<span style="color: gray">.</span>[Count] <span style="color: blue">desc</span><span style="color: gray">, </span>ob2<span style="color: gray">.</span>[DateDiffInDays] <span style="color: blue">asc</span><span style="color: gray">) </span><span style="color: blue">as </span>[RowNumber]<span style="color: gray">,
            </span>[Count]<span style="color: gray">,
            </span>[DateDiffInDays]<span style="color: gray">,
            </span>[Postcode]<span style="color: gray">,
            </span>[TimeSpanId]
        <span style="color: blue">from 
        </span><span style="color: gray">(
            </span><span style="color: blue">select
                </span><span style="color: magenta">sum</span><span style="color: gray">(</span>ob<span style="color: gray">.</span>[Count]<span style="color: gray">) </span><span style="color: blue">as </span>[Count]<span style="color: gray">,
                </span><span style="color: magenta">sum</span><span style="color: gray">(</span><span style="color: magenta">datediff</span><span style="color: gray">(</span><span style="color: magenta">day</span><span style="color: gray">, </span>ob<span style="color: gray">.</span>[Date]<span style="color: gray">, </span>@DateNow<span style="color: gray">) * </span>ob<span style="color: gray">.</span>[Count]<span style="color: gray">) </span><span style="color: blue">as </span>[DateDiffInDays]<span style="color: gray">,
                </span>ob<span style="color: gray">.</span>[Postcode]<span style="color: gray">,
                </span>ob<span style="color: gray">.</span>[TimeSpanId]
            <span style="color: blue">from </span>Observation ob
            <span style="color: gray">inner join </span>TimeSpan ts <span style="color: blue">on </span>ob<span style="color: gray">.</span>TimeSpanId <span style="color: gray">= </span>ts<span style="color: gray">.</span>Id
            <span style="color: blue">group by </span>ob<span style="color: gray">.</span>[Postcode]<span style="color: gray">, </span>ob<span style="color: gray">.</span>[TimeSpanId]
        <span style="color: gray">) </span>ob2
    <span style="color: gray">) </span>ob3
    <span style="color: blue">where </span>ob3<span style="color: gray">.</span>[RowNumber] <span style="color: gray">= </span>1
<span style="color: gray">) </span>ob4
<span style="color: blue">on </span>ts<span style="color: gray">.</span>[Id] <span style="color: gray">= </span>ob4<span style="color: gray">.</span>[TimeSpanId]</pre>


<p>&#160;</p>

<p><strong>Result</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/07/image1.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/07/image_thumb1.png" width="563" height="127" /></a></p>