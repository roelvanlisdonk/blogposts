---
ID: 707
post_title: 'Export images from SQL Server database with C# 3.5'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/09/15/export-images-from-sql-server-database-with-c-3-5/
published: true
post_date: 2009-09-15 14:02:57
---
<p>If you want to export images from a SQL Server database you could use the following code:   <br />    <br /></p>  <pre class="code"><span style="color: blue">        public void </span>ExportImagesFromDatabase()
        {
            <span style="color: blue">var </span>exportPath = <span style="color: #a31515">@&quot;C:\Temp&quot;</span>;
            <span style="color: blue">if </span>(!<span style="color: #2b91af">Directory</span>.Exists(exportPath))
            {
                <span style="color: #2b91af">Directory</span>.CreateDirectory(exportPath);
            }
            <span style="color: blue">var </span>imagesTable = GetImagesFromDatabase(<span style="color: #a31515">&quot;select [ImageColumn] from [ImageTable]&quot;</span>);
            <span style="color: blue">var </span>rowCounter = 0;
            <span style="color: blue">foreach </span>(<span style="color: #2b91af">DataRow </span>row <span style="color: blue">in </span>imagesTable.Rows)
            {
                <span style="color: blue">if </span>(row.ItemArray.Length &gt; 0)
                {
                    <span style="color: blue">if </span>(row[0] != <span style="color: blue">null</span>)
                    {
                        <span style="color: blue">var </span>imageBytes = (<span style="color: blue">byte</span>[])row[<span style="color: #a31515">&quot;Image&quot;</span>];
                        <span style="color: blue">if </span>(imageBytes.Length &gt; 0)
                        {
                            <span style="color: blue">using </span>(<span style="color: blue">var </span>convertedImage = <span style="color: blue">new </span><span style="color: #2b91af">Bitmap</span>(<span style="color: blue">new </span><span style="color: #2b91af">MemoryStream</span>(imageBytes)))
                            {
                                <span style="color: blue">var </span>fileName = <span style="color: #2b91af">Path</span>.Combine(exportPath, <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;ExportImage_{0}.bmp&quot;</span>, rowCounter.ToString().PadLeft(5, <span style="color: #a31515">'0'</span>)));
                                <span style="color: blue">if </span>(<span style="color: #2b91af">File</span>.Exists(fileName))
                                {
                                    <span style="color: #2b91af">File</span>.Delete(fileName);
                                }
                                convertedImage.Save(fileName);
                            }
                        }
                    }
                }
            }
        }
        <span style="color: blue">public </span><span style="color: #2b91af">DataTable </span>GetImagesFromDatabase(<span style="color: blue">string </span>query)
        {
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(query))
            {
                <span style="color: blue">throw new </span><span style="color: #2b91af">NullReferenceException</span>(<span style="color: #a31515">&quot;Parameter query can't be null or empty&quot;</span>);
            }
            <span style="color: blue">var </span>result = <span style="color: blue">new </span><span style="color: #2b91af">DataTable</span>();
            <span style="color: blue">using </span>(<span style="color: blue">var </span>connection = <span style="color: blue">new </span><span style="color: #2b91af">SqlConnection</span>(<span style="color: #2b91af">ConfigurationManager</span>.ConnectionStrings[<span style="color: #a31515">&quot;Runner&quot;</span>].ConnectionString))
            {
                <span style="color: blue">using </span>(<span style="color: blue">var </span>command = <span style="color: blue">new </span><span style="color: #2b91af">SqlCommand</span>(query, connection))
                {
                    connection.Open();
                    command.CommandTimeout = 0;
                    command.CommandType = <span style="color: #2b91af">CommandType</span>.Text;

                    <span style="color: blue">using </span>(<span style="color: blue">var </span>adapter = <span style="color: blue">new </span><span style="color: #2b91af">SqlDataAdapter</span>(command))
                    {
                        <span style="color: blue">var </span>recordCount = adapter.Fill(result);
                    }
                }
            }

            <span style="color: blue">return </span>result;
        }</pre>
<a href="http://11011.net/software/vspaste"></a>