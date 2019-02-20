---
ID: 3393
post_title: >
  Execute a stored procedure for each row
  without using a cursor in T-SQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/09/09/execute-stored-procedure-for-each-row-without-cursor-in-t-sql/
published: true
post_date: 2013-09-09 14:45:26
---
<p>If you want to execute a stored procedure for each row in T-SQL 2012, where the Id column is not a consecutive number, you van use the following T-SQL code</p>  <p>&#160;</p>  <p><strong>SQL Server &gt;= 2012</strong></p>  <pre class="code"><span style="color: blue">declare </span><span style="color: teal">@Person </span><span style="color: blue">table
</span><span style="color: gray">(
    </span><span style="color: teal">Id          </span><span style="color: blue">int                </span><span style="color: gray">not null,
    </span><span style="color: teal">Name        </span><span style="color: blue">varchar</span><span style="color: gray">(</span><span style="color: magenta">max</span><span style="color: gray">)    not null
)

</span><span style="color: blue">insert into </span><span style="color: teal">@Person </span><span style="color: blue">values
    </span><span style="color: gray">(</span>1<span style="color: gray">, </span><span style="color: red">'John'</span><span style="color: gray">),
    (</span>4<span style="color: gray">, </span><span style="color: red">'Mike'</span><span style="color: gray">)


</span><span style="color: green">-- Determine loop boundaries.
</span><span style="color: blue">declare </span><span style="color: teal">@Id </span><span style="color: blue">int </span><span style="color: gray">= </span>0
<span style="color: blue">declare </span><span style="color: teal">@counter </span><span style="color: blue">int </span><span style="color: gray">= </span>0
<span style="color: blue">declare </span><span style="color: teal">@total </span><span style="color: blue">int </span><span style="color: gray">= </span><span style="color: magenta">isnull</span><span style="color: gray">((</span><span style="color: blue">select </span><span style="color: magenta">count</span><span style="color: gray">(</span>1<span style="color: gray">) </span><span style="color: blue">from </span><span style="color: teal">@Person</span><span style="color: gray">), </span>0<span style="color: gray">)
    
</span><span style="color: green">-- Iterate records.
</span><span style="color: blue">while </span><span style="color: gray">(</span><span style="color: teal">@counter </span><span style="color: gray">&lt;&gt; (</span><span style="color: teal">@total</span><span style="color: gray">))
</span><span style="color: blue">begin  
        </span><span style="color: green">-- record to proces.
        </span><span style="color: blue">set </span><span style="color: teal">@Id </span><span style="color: gray">= (</span><span style="color: blue">select </span><span style="color: teal">Id </span><span style="color: blue">from </span><span style="color: teal">@Person </span><span style="color: blue">order by </span><span style="color: teal">Id offset @counter </span><span style="color: blue">rows fetch next </span>1 <span style="color: blue">rows </span><span style="color: teal">only</span><span style="color: gray">)

        </span><span style="color: green">-- Exec sproc here:
        </span><span style="color: blue">select </span><span style="color: teal">@Id
                    
        </span><span style="color: green">-- Increase counter to break the loop after all records are processed.
        </span><span style="color: blue">set </span><span style="color: teal">@counter </span><span style="color: gray">= </span><span style="color: teal">@counter </span><span style="color: gray">+ </span>1
<span style="color: blue">end
</span></pre>
If however you are stuck on SQL Server before 2012 and your Id’s are consecutive you can use the following code:

<p>&#160;</p>

<p><strong>SQL Server &lt; 2012</strong></p>

<p>&#160;</p>

<pre class="code"><span style="color: blue">declare </span><span style="color: teal">@Person </span><span style="color: blue">table
</span><span style="color: gray">(
    </span><span style="color: teal">Id            </span><span style="color: blue">int                </span><span style="color: gray">not null </span><span style="color: blue">identity</span><span style="color: gray">(</span>1<span style="color: gray">,</span>1<span style="color: gray">),
    </span><span style="color: teal">Name        </span><span style="color: blue">varchar</span><span style="color: gray">(</span><span style="color: magenta">max</span><span style="color: gray">)    not null
)

</span><span style="color: blue">insert into </span><span style="color: teal">@Person </span><span style="color: blue">values 
    </span><span style="color: gray">(</span><span style="color: red">'John'</span><span style="color: gray">),
    (</span><span style="color: red">'Mike'</span><span style="color: gray">)

</span><span style="color: green">-- Determine first record to process.
</span><span style="color: blue">declare </span><span style="color: teal">@Id </span><span style="color: blue">int </span><span style="color: gray">= (</span><span style="color: blue">select </span><span style="color: magenta">min</span><span style="color: gray">(</span><span style="color: teal">Id</span><span style="color: gray">) </span><span style="color: blue">from </span><span style="color: teal">@Person</span><span style="color: gray">)

</span><span style="color: green">-- Iterate records.
</span><span style="color: blue">while </span><span style="color: gray">(</span><span style="color: teal">@Id </span><span style="color: gray">is not null) 
</span><span style="color: blue">begin  
</span><span style="color: gray">    
    </span><span style="color: green">-- Exec sproc here:
    </span><span style="color: blue">select    </span><span style="color: teal">Name
    </span><span style="color: blue">from    </span><span style="color: teal">@Person
    </span><span style="color: blue">where    </span><span style="color: teal">Id </span><span style="color: gray">= </span><span style="color: teal">@Id
            
    </span><span style="color: green">-- Select next record, this will break the loop if next record is not found.
    </span><span style="color: blue">set </span><span style="color: teal">@Id </span><span style="color: gray">= (</span><span style="color: blue">select </span><span style="color: teal">Id </span><span style="color: blue">from </span><span style="color: teal">@Person </span><span style="color: blue">where </span><span style="color: teal">Id </span><span style="color: gray">= </span><span style="color: teal">@Id </span><span style="color: gray">+ </span>1<span style="color: gray">)
</span><span style="color: blue">end
</span></pre>