---
ID: 1907
post_title: >
  How to search for a value, in all
  columns of a Microsoft SQL Server
  Database
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/02/07/how-to-search-for-a-value-in-all-columns-of-a-microsoft-sql-server-database/
published: true
post_date: 2011-02-07 16:55:08
---
<p>If you want to search in for a specific value in all columns of a Microsoft SQL Server Database, you can use the following T-SQL stored procedure:</p> <p>&nbsp;</p><pre class="code"><span style="color: blue">CREATE PROC SearchAllTables</span><span style="color: gray">(  
        @SearchStr </span><span style="color: blue">nvarchar</span><span style="color: gray">(100)  
 ) </span><span style="color: blue">AS  
 BEGIN  
        CREATE TABLE #Results </span><span style="color: gray">(ColumnName </span><span style="color: blue">nvarchar</span><span style="color: gray">(370), ColumnValue </span><span style="color: blue">nvarchar</span><span style="color: gray">(3630))  
        </span><span style="color: blue">SET NOCOUNT ON  
        DECLARE @TableName nvarchar</span><span style="color: gray">(256), @ColumnName </span><span style="color: blue">nvarchar</span><span style="color: gray">(128), @SearchStr2 </span><span style="color: blue">nvarchar</span><span style="color: gray">(110)  
        </span><span style="color: blue">SET  @TableName </span><span style="color: gray">= </span><span style="color: red">''  
        </span><span style="color: blue">SET @SearchStr2 </span><span style="color: gray">= </span><span style="color: magenta">QUOTENAME</span><span style="color: gray">(</span><span style="color: red">'%' </span><span style="color: gray">+ @SearchStr + </span><span style="color: red">'%'</span><span style="color: gray">,</span><span style="color: red">''''</span><span style="color: gray">)  
   
        </span><span style="color: blue">WHILE @TableName </span><span style="color: gray">IS NOT NULL  
        </span><span style="color: blue">BEGIN  
                SET @ColumnName </span><span style="color: gray">= </span><span style="color: red">''  
                </span><span style="color: blue">SET @TableName </span><span style="color: gray">=  
                (  
                        </span><span style="color: blue">SELECT </span><span style="color: magenta">MIN</span><span style="color: gray">(</span><span style="color: magenta">QUOTENAME</span><span style="color: gray">(TABLE_SCHEMA) + </span><span style="color: red">'.' </span><span style="color: gray">+ </span><span style="color: magenta">QUOTENAME</span><span style="color: gray">(TABLE_NAME))  
                        </span><span style="color: blue">FROM    </span><span style="color: green">INFORMATION_SCHEMA</span><span style="color: gray">.</span><span style="color: green">TABLES  
                        </span><span style="color: blue">WHERE           TABLE_TYPE </span><span style="color: gray">= </span><span style="color: red">'BASE TABLE'  
                                </span><span style="color: gray">AND     </span><span style="color: magenta">QUOTENAME</span><span style="color: gray">(TABLE_SCHEMA) + </span><span style="color: red">'.' </span><span style="color: gray">+ </span><span style="color: magenta">QUOTENAME</span><span style="color: gray">(TABLE_NAME) &gt; @TableName  
                                AND     </span><span style="color: magenta">OBJECTPROPERTY</span><span style="color: gray">(  
                                                </span><span style="color: magenta">OBJECT_ID</span><span style="color: gray">(  
                                                        </span><span style="color: magenta">QUOTENAME</span><span style="color: gray">(TABLE_SCHEMA) + </span><span style="color: red">'.' </span><span style="color: gray">+ </span><span style="color: magenta">QUOTENAME</span><span style="color: gray">(TABLE_NAME)  
                                                         ), </span><span style="color: red">'IsMSShipped'  
                                                       </span><span style="color: gray">) = 0  
                )  
                </span><span style="color: blue">WHILE </span><span style="color: gray">(@TableName IS NOT NULL) AND (@ColumnName IS NOT NULL)  
                </span><span style="color: blue">BEGIN  
                        SET @ColumnName </span><span style="color: gray">=  
                        (  
                                </span><span style="color: blue">SELECT </span><span style="color: magenta">MIN</span><span style="color: gray">(</span><span style="color: magenta">QUOTENAME</span><span style="color: gray">(COLUMN_NAME))  
                                </span><span style="color: blue">FROM    </span><span style="color: green">INFORMATION_SCHEMA</span><span style="color: gray">.</span><span style="color: green">COLUMNS  
                                </span><span style="color: blue">WHERE           TABLE_SCHEMA    </span><span style="color: gray">= </span><span style="color: magenta">PARSENAME</span><span style="color: gray">(@TableName, 2)  
                                        AND     TABLE_NAME      = </span><span style="color: magenta">PARSENAME</span><span style="color: gray">(@TableName, 1)  
                                        AND     DATA_TYPE IN (</span><span style="color: red">'char'</span><span style="color: gray">, </span><span style="color: red">'varchar'</span><span style="color: gray">, </span><span style="color: red">'nchar'</span><span style="color: gray">, </span><span style="color: red">'nvarchar'</span><span style="color: gray">)  
                                        AND     </span><span style="color: magenta">QUOTENAME</span><span style="color: gray">(COLUMN_NAME) &gt; @ColumnName  
                        )  
                        </span><span style="color: blue">IF @ColumnName </span><span style="color: gray">IS NOT NULL  
                        </span><span style="color: blue">BEGIN  
                                INSERT INTO #Results  
                                EXEC  
                                </span><span style="color: gray">(  
                                        </span><span style="color: red">'SELECT ''' </span><span style="color: gray">+ @TableName + </span><span style="color: red">'.' </span><span style="color: gray">+ @ColumnName + </span><span style="color: red">''', LEFT(' </span><span style="color: gray">+ @ColumnName + </span><span style="color: red">', 3630)  
                                        FROM ' </span><span style="color: gray">+ @TableName + </span><span style="color: red">' (NOLOCK) ' </span><span style="color: gray">+  
                                        </span><span style="color: red">' WHERE ' </span><span style="color: gray">+ @ColumnName + </span><span style="color: red">' LIKE ' </span><span style="color: gray">+ @SearchStr2  
                                )  
                        </span><span style="color: blue">END  
                END  
        END  
        SELECT ColumnName</span><span style="color: gray">, ColumnValue </span><span style="color: blue">FROM #Results  
        drop table #Results
 END  
</pre></span>