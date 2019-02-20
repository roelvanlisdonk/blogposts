---
ID: 3342
post_title: >
  How to handle variable column count with
  the SSIS 2008 Flat File Source.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/08/28/how-to-handle-variable-column-count-with-the-ssis-2008-flat-file-source/
published: true
post_date: 2013-08-28 14:35:20
---
<p>If you want to import flat files (e.g. *.csv) that contain rows with dynamic column count, the best way is to use this codeplex component: <a href="http://ssisdfs.codeplex.com/">http://ssisdfs.codeplex.com/</a></p>  <p>&#160;</p>  <p>If you don’t want to use that component, here is a script task that alters the import file, before the flat file source executes.</p>  <p>&#160;</p>  <p>&#160;</p>  <pre class="code"><span style="color: blue">public void </span>Main()
{
    Dts.TaskResult = (<span style="color: blue">int</span>)<span style="color: #2b91af">ScriptResults</span>.Success;

    <span style="color: green">// Files should contain 46 columns
    </span><span style="color: blue">int </span>maxColumnCount = 46;

    <span style="color: green">// Determines if an event can be fired more than once for the duration of the current execution.
    </span><span style="color: #2b91af">Boolean </span>fireAgain = <span style="color: blue">true</span>;

    Dts.Events.FireInformation(0, <span style="color: #a31515">&quot;Info: &quot;</span>, <span style="color: #a31515">&quot;Update file process started (update file so it contains the correct column count per row).&quot;</span>, <span style="color: blue">string</span>.Empty, 0, <span style="color: blue">ref </span>fireAgain);

    <span style="color: green">// Get file path.
    </span><span style="color: blue">string </span>importFile = Dts.Variables[<span style="color: #a31515">@&quot;User::FileToImport&quot;</span>].Value.ToString();

    <span style="color: green">// Check if file exists.
    </span><span style="color: blue">if </span>(System.IO.<span style="color: #2b91af">File</span>.Exists(importFile))
    {
        <span style="color: green">// Will contain the new file content with corrected column count.
        </span><span style="color: blue">var </span>newFileContents = <span style="color: blue">new </span>System.Text.<span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);

        <span style="color: blue">using </span>(<span style="color: blue">var </span>streamReader = <span style="color: blue">new </span>System.IO.<span style="color: #2b91af">StreamReader</span>(spiFile))
        {
            <span style="color: green">// Continue reading until end of file.
            </span><span style="color: blue">while </span>(!streamReader.EndOfStream)
            {
                <span style="color: green">// Read a line.
                </span><span style="color: blue">string </span>line = streamReader.ReadLine();

                <span style="color: green">// Ignore empty lines (empty lines will not be added to the new file contents).
                </span><span style="color: blue">if </span>(!<span style="color: blue">string</span>.IsNullOrEmpty(line))
                {
                    <span style="color: green">// Split on &quot;,&quot;, so we can count columns. Use string[] for performance reasons (later the array is used to join).
                    </span><span style="color: blue">string</span>[] lineColumns = line.Split(<span style="color: #a31515">','</span>);

                    <span style="color: green">// Check if current row contains less columns, then max column count.
                    </span><span style="color: blue">bool </span>lessColumns = (lineColumns.Length &lt; maxColumnCount);

                    <span style="color: blue">if </span>(lessColumns)
                    {
                        <span style="color: green">// Add column until maxColumnCount.
                        </span><span style="color: #2b91af">Array</span>.Resize(<span style="color: blue">ref </span>lineColumns, maxColumnCount);
                    }

                    <span style="color: green">// Store only max column count in new file contents (ignoring extra columns).
                    </span><span style="color: blue">string </span>newLine = <span style="color: blue">string</span>.Join(<span style="color: #a31515">&quot;,&quot;</span>, lineColumns, 0, maxColumnCount);
                    newFileContents.AppendLine(newLine);
                }
            }
        }

        <span style="color: green">// Save new file contents.
        </span>System.IO.<span style="color: #2b91af">File</span>.WriteAllText(importFile, newFileContents.ToString());
    }
    <span style="color: blue">else
    </span>{
        Dts.Events.FireInformation(0, <span style="color: #a31515">&quot;Info: &quot;</span>, <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;File: {0} not found.&quot;</span>, importFile), <span style="color: blue">string</span>.Empty, 0, <span style="color: blue">ref </span>fireAgain);
        Dts.TaskResult = (<span style="color: blue">int</span>)<span style="color: #2b91af">ScriptResults</span>.Failure;
    }

    Dts.Events.FireInformation(0, <span style="color: #a31515">&quot;Info: &quot;</span>, <span style="color: #a31515">&quot;Update file process completed.&quot;</span>, <span style="color: blue">string</span>.Empty, 0, <span style="color: blue">ref </span>fireAgain);
}</pre>