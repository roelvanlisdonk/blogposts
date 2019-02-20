---
ID: 987
post_title: 'How to automatically determine the installation order / sequence of TSQL table scripts with foreignkeys by using C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/01/14/how-to-automatically-determine-the-installation-order-sequence-of-tsql-table-scripts-with-foreignkeys-by-using-c/
published: true
post_date: 2010-01-14 13:50:03
---
<p>If you have a folder with (*.sql) TSQL table scripts and you want to deploy these scripts, you can manually add the file names by adding numbers to set the order of installation.   <br />    <br />001. Cars.sql    <br />002. Customers.sql    <br />etc.    <br />    <br />Or you can use a C# function to automatically determine the installation order of the TSQL table scripts:</p>  <pre class="code"><span style="color: blue">public void </span>ExecuteTableTSQLScriptFiles(<span style="color: blue">string </span>server, <span style="color: blue">string </span>database, <span style="color: blue">string </span>userId, <span style="color: blue">string </span>password, <span style="color: blue">bool </span>trustedConnection, <span style="color: blue">string </span>folder)
    {
      <span style="color: green">// Validate parameters
      </span><span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(server)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;server&quot;</span>); }
      <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(database)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;database&quot;</span>); }
      <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(userId)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;userId&quot;</span>); }
      <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(password)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;password&quot;</span>); }
      <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(folder)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;folder&quot;</span>); }
      <span style="color: blue">if </span>(!<span style="color: #2b91af">Directory</span>.Exists(folder)) { <span style="color: blue">new </span><span style="color: #2b91af">ApplicationException</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;Folder [{0]] does not exist&quot;</span>, folder)); }

      <span style="color: green">// Get *.sql files in folder
      </span><span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt; filesToProcess = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt;();
      filesToProcess.AddRange(<span style="color: #2b91af">Directory</span>.GetFiles(folder, <span style="color: #a31515">&quot;*.sql&quot;</span>));

      <span style="color: green">// First loop will install all tables with no foreignkeys
      // Second loop will install all tables with foreignkeys that are not part of a foreignkey
      // Preceding loops will install all tables with foreignkeys that are part of a foreignekey
      // Use loopCounter to prevent endless loop
      </span><span style="color: blue">int </span>loopCounter = 0;
      <span style="color: blue">while </span>(filesToProcess.Count() &gt; 0 &amp;&amp; loopCounter &lt;= 10)
      {
        <span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt; reProcessFiles = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt;();
        <span style="color: blue">foreach </span>(<span style="color: blue">string </span>file <span style="color: blue">in </span>filesToProcess)
        {
          <span style="color: blue">try
          </span>{
              <span style="color: green">// Get script file contents
            </span><span style="color: blue">string </span>scriptContents = <span style="color: #2b91af">File</span>.ReadAllText(file);

            <span style="color: green">// Make sure alle GO statements are capatilized
            </span>scriptContents = scriptContents.Replace(<span style="color: #a31515">&quot;\r\ngo\r\n&quot;</span>, <span style="color: #a31515">&quot;\r\nGO\r\n&quot;</span>);

            <span style="color: green">// Remove leading and trailing spaces
            </span>scriptContents = scriptContents.Trim();

            <span style="color: green">// Determine if file contents ends with go statement
            </span><span style="color: blue">if </span>(scriptContents.EndsWith(<span style="color: #a31515">&quot;go&quot;</span>) || scriptContents.EndsWith(<span style="color: #a31515">&quot;GO&quot;</span>))
            {
              <span style="color: green">// Remvove last go statement
              </span>scriptContents = scriptContents.Remove(scriptContents.Length - 2);
            }

            <span style="color: green">//split the script on &quot;GO&quot; commands
            </span><span style="color: blue">string</span>[] splitter = <span style="color: blue">new string</span>[] { <span style="color: #a31515">&quot;\r\nGO\r\n&quot; </span>};
            <span style="color: blue">string</span>[] commandTexts = scriptContents.Split(splitter, <span style="color: #2b91af">StringSplitOptions</span>.RemoveEmptyEntries);

            <span style="color: green">// Determine connection string
            </span><span style="color: blue">string </span>connectionString = <span style="color: blue">string</span>.Format(<span style="color: #a31515">@&quot;Server=&quot;&quot;{0}&quot;&quot;;Database=&quot;&quot;{1}&quot;&quot;;User ID=&quot;&quot;{2}&quot;&quot;;Password=&quot;&quot;{3}&quot;&quot;;Trusted_Connection={4};&quot;</span>, server, database, userId, password, trustedConnection);

            <span style="color: green">// Run each sql command in the sql script file
            </span><span style="color: blue">foreach </span>(<span style="color: blue">string </span>commandText <span style="color: blue">in </span>commandTexts)
            {
              <span style="color: blue">using </span>(<span style="color: #2b91af">SqlConnection </span>sqlConnection = <span style="color: blue">new </span><span style="color: #2b91af">SqlConnection</span>(connectionString))
              {
                <span style="color: blue">using </span>(<span style="color: #2b91af">SqlCommand </span>command = <span style="color: blue">new </span><span style="color: #2b91af">SqlCommand</span>(commandText, sqlConnection))
                {
                  command.Connection.Open();
                  command.ExecuteNonQuery();
                }
              }
            }

          }
          <span style="color: blue">catch </span>(<span style="color: #2b91af">Exception </span>ex)
          {
            <span style="color: green">// Add as first file to reProcessFiles, when exception starts with [Foreign key]
            </span><span style="color: blue">if </span>(!<span style="color: blue">string</span>.IsNullOrEmpty(ex.Message) &amp;&amp; ex.Message.StartsWith(<span style="color: #a31515">&quot;Foreign key&quot;</span>))
            {
              reProcessFiles.Insert(0, file);
            }
          }
        }

        filesToProcess = reProcessFiles;
        loopCounter++;
      }
    }</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>
  <br /><strong><font size="4">It’s a dirty function but somebody had to make it ;-)</font></strong></p>