---
ID: 3378
post_title: >
  Implement conditional (IF THEN ELSE)
  logic based on a SQL Server Store
  Procedure result in SSIS 2012
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/09/04/implement-conditional-if-then-else-logic-based-on-a-sql-server-store-procedure-result-in-ssis-2012/
published: true
post_date: 2013-09-04 12:22:49
---
<p>There are many ways you could implement conditional (IF THEN ELSE) logic based on a SQL Server Store Procedure result in SSIS, here is just one way:</p> <p>&nbsp;</p> <p>Note</p> <p>For demo purpose I will be using the master database here. </p> <p>&nbsp;</p> <p><strong>Stored Procedure</strong></p> <p>Create sproc on master database</p><pre class="code"><span style="color: blue">if  </span><span style="color: magenta">object_id</span><span style="color: gray">(</span><span style="color: red">'dbo.ColumnExists'</span><span style="color: gray">) is not null
</span><span style="color: blue">begin
    drop procedure </span><span style="color: teal">dbo</span><span style="color: gray">.</span><span style="color: teal">ColumnExists
</span><span style="color: blue">end
go

</span><span style="color: green">-- Determines if the given column exists in the given table.
</span><span style="color: blue">create procedure </span><span style="color: teal">dbo</span><span style="color: gray">.</span><span style="color: teal">ColumnExists
    @TableName </span><span style="color: blue">varchar</span><span style="color: gray">(128), </span><span style="color: green">-- Full table name, like dbo.MyTable
    </span><span style="color: teal">@ColumnName </span><span style="color: blue">varchar</span><span style="color: gray">(128)
</span><span style="color: blue">as
begin
    set nocount on
    
    declare </span><span style="color: teal">@ColumnExistsResult </span><span style="color: blue">bit </span><span style="color: gray">= 0

    </span><span style="color: green">-- Check if table exists.
    </span><span style="color: blue">if </span><span style="color: gray">exists (</span><span style="color: blue">select top 1 1 from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">objects </span><span style="color: blue">where </span><span style="color: magenta">Object_ID </span><span style="color: gray">= </span><span style="color: magenta">Object_ID</span><span style="color: gray">(</span><span style="color: teal">@TableName</span><span style="color: gray">)) 
    </span><span style="color: blue">begin 
        </span><span style="color: green">-- Check if column exists in table.
        </span><span style="color: blue">if </span><span style="color: gray">exists (</span><span style="color: blue">select top 1 1 from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">columns </span><span style="color: blue">where </span><span style="color: teal">name </span><span style="color: gray">= </span><span style="color: teal">@ColumnName </span><span style="color: gray">and </span><span style="color: magenta">Object_ID </span><span style="color: gray">= </span><span style="color: magenta">Object_ID</span><span style="color: gray">(</span><span style="color: teal">@TableName</span><span style="color: gray">)) 
        </span><span style="color: blue">begin 
            set </span><span style="color: teal">@ColumnExistsResult </span><span style="color: gray">= 1
        </span><span style="color: blue">end
    end

    </span><span style="color: green">-- Return single row to SSIS.
    </span><span style="color: blue">select </span><span style="color: teal">@ColumnExistsResult </span><span style="color: blue">as </span><span style="color: teal">ColumnExistsResult </span><span style="color: green">-- This name should be used as ResultSet name in 
</span><span style="color: blue">end
go
</pre></span>
<p><strong>Add connection</strong></p>
<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image_thumb.png" width="580" height="595"></a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>Add package variables</strong></p>
<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image_thumb1.png" width="580" height="129"></a></p>
<p>&nbsp;</p>
<p>For demo purposes I entered a default value for TableName ("dbo.spt_monitor") and ColumnName ("lastrun").</p>
<p>&nbsp;</p>
<p><strong>Add Execute SQL Task</strong></p>
<p>Change Connection to the name of connection created in the previous step.</p>
<p>Change ResultSet to "Singel row"</p>
<p>Change SQLSourceType to "Direct input", so the task will use the t-sql query in the property "SQL Statement"</p>
<p>Change SQLStatement to "exec dbo.ColunExists ?, ?"</p>
<p>Note multiple parameters should be separated by ",".</p>
<p>&nbsp;</p>
<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image2.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image_thumb2.png" width="580" height="494"></a></p>
<p>&nbsp;</p>
<p><strong>Add parameter mapping</strong></p>
<p>De parameters are linked to the question marks in the SQL Statement.</p>
<p>The first "?" in exec dbo.ColumnExists will be linked to Parameter Name "0" on the Parameter Mapping page.</p>
<p>Note on Date Type (data type "DATE" is datetime in t-sql, data type VARIANT_BOOL" is t-sql data type bit).</p>
<p>&nbsp;</p>
<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image3.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image_thumb3.png" width="580" height="494"></a></p>
<p>&nbsp;</p>
<p><strong>Setting Result Set</strong></p>
<p>On the Result Set page you&nbsp; can map the column names from the stored procedure call to SSIS package variables.</p>
<p>&nbsp;</p>
<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image4.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image_thumb4.png" width="580" height="494"></a></p>
<p>&nbsp;</p>
<p><strong>Setting the values for the precedence constraints</strong></p>
<p>If&nbsp; you want a data flow to be executed, when the "Execute SQL Task" fails or the given column does not exists, you should set the precedence constraint as follow:</p>
<p>&nbsp;</p>
<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image5.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image_thumb5.png" width="580" height="434"></a></p>
<p>&nbsp;</p>
<p>If you want a data flow to be executed, when the "Execute SQL Task" succeeds and the given column exists, you should set the precedence constraint as follow:</p>
<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image6.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image_thumb6.png" width="580" height="434"></a></p>
<p>&nbsp;</p>
<p>The end result should look like</p>
<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image7.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image_thumb7.png" width="580" height="110"></a></p>

<p>When we execute the package and the column exists the debugger should be paused on the left data flow:</p>
<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image8.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image_thumb8.png" width="580" height="119"></a></p>
<p>&nbsp;</p>
<p>When the column does not exist the debugger should be paused at the right dataflow:</p>
<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image9.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image_thumb9.png" width="580" height="105"></a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>When the "execute sql task" fails the debugger will be paused at the left dataflow:</p>
<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image10.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image_thumb10.png" width="580" height="126"></a></p>