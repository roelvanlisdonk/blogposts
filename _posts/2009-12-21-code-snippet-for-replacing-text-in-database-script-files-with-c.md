---
ID: 866
post_title: 'Code snippet for replacing text in database script files with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/21/code-snippet-for-replacing-text-in-database-script-files-with-c/
published: true
post_date: 2009-12-21 09:56:31
---
<p>For deploying database content, we use database script files (TSQL *.sql). When the structure of the database changes, these script must be adjusted. To change the script I use a NUnit test, that looks like:</p>  <pre class="code"><span style="color: #2b91af">            StringBuilder </span>result = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);

            <span style="color: green">// Read the contents of the file
            </span><span style="color: blue">string </span>fileContents = <span style="color: #2b91af">File</span>.ReadAllText(<span style="color: #a31515">@&quot;..\..\..\MyDatabaseProject\Contents\Customer.sql&quot;</span>);

            <span style="color: green">// Split in lines
            </span><span style="color: blue">string</span>[] lines = fileContents.Split(<span style="color: blue">new string</span>[] { <span style="color: #2b91af">Environment</span>.NewLine }, <span style="color: #2b91af">StringSplitOptions</span>.RemoveEmptyEntries);

            <span style="color: green">// Loop lines
            </span><span style="color: blue">foreach </span>(<span style="color: blue">string </span>line <span style="color: blue">in </span>lines)
            {
                <span style="color: green">// Determine if line starts with
                </span><span style="color: blue">if </span>(line.StartsWith(<span style="color: #a31515">&quot;insert into Customer &quot;</span>))
                {
                    <span style="color: green">// Adjust line
                    </span><span style="color: blue">string </span>adjustedLine = line.Insert(76, <span style="color: #a31515">&quot;'&quot;</span>);
                    adjustedLine = adjustedLine.Insert(81, <span style="color: #a31515">&quot;AA'&quot;</span>);
                    adjustedLine = adjustedLine.Insert(85, <span style="color: #a31515">&quot;'&quot;</span>);
                    adjustedLine = adjustedLine.Insert(90, <span style="color: #a31515">&quot;ZZ'&quot;</span>);

                    <span style="color: green">// Add adjusted line to output
                    </span>result.AppendLine(adjustedLine);
                }
                <span style="color: blue">else
                </span>{
                    <span style="color: green">// Add line to output
                    </span>result.AppendLine(line);
                }
            }

            <span style="color: #2b91af">Console</span>.Write(result.ToString());</pre>
<a href="http://11011.net/software/vspaste"></a>