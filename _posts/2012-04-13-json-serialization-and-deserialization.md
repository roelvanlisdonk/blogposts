---
ID: 2654
post_title: JSON Serialization and Deserialization
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/04/13/json-serialization-and-deserialization/
published: true
post_date: 2012-04-13 14:40:48
---
<p>Found a good articale on JSON Serialization and Deserialization:</p>  <p><a href="http://www.codeproject.com/Articles/272335/JSON-Serialization-and-Deserialization-in-ASP-NET">http://www.codeproject.com/Articles/272335/JSON-Serialization-and-Deserialization-in-ASP-NET</a></p>  <p>I used this article to create a class that serializes DataSet, DataTable and DataRow objects:</p>  <p>I just changed one aspect of the codeproject article, I used the regular expression &quot;\\/Date\((-?\d+)\)\\/&quot; instead of&#160; “\\/Date\((\d+)\+\d+\)\\/”. The regular expression “\\/Date\((-?\d+)\)\\/” takes into account dates before epoch (1979-1-1).</p>  <pre class="code"><span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">Contains JSON helper functions.
</span><span style="color: gray">/// &lt;/summary&gt;
</span><span style="color: blue">public class </span><span style="color: #2b91af">JsonHelper
</span>{
    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">Date time format, used to convert a datetime to a string.
    </span><span style="color: gray">/// </span><span style="color: green">By default &quot;yyyy-MM-dd HH:mm:ss&quot;.
    </span><span style="color: gray">/// &lt;/summary&gt;
    </span><span style="color: blue">public string </span>DateTimeFormat { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }

    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">Initializes properties.
    </span><span style="color: gray">/// &lt;/summary&gt;
    </span><span style="color: blue">public </span>JsonHelper()
    {
        DateTimeFormat = <span style="color: #a31515">&quot;yyyy-MM-dd HH:mm:ss&quot;</span>;
    }

    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">Converts a DataSet to a JSON string.
    </span><span style="color: gray">/// &lt;/summary&gt;
    /// &lt;param name=&quot;dataSet&quot;&gt;</span><span style="color: green">The dataset to convert.</span><span style="color: gray">&lt;/param&gt;
    /// &lt;exception cref=&quot;System.ArgumentException&quot;&gt;</span><span style="color: green">Thrown when parameter [dataSet] is null.</span><span style="color: gray">&lt;/exception&gt;
    /// &lt;returns&gt;
    /// </span><span style="color: green">- JSON in the format [[[Table0Row0Column0,Table0Row0Column1],[Table0Row1Column0,Table0Row1Column1]],[[Table1Row0Column0,Table1Row0Column1],[Table1Row1Column0,Table1Row1Column1]]]
    </span><span style="color: gray">/// </span><span style="color: green">- Empty string, when dataset contains no tables.
    </span><span style="color: gray">/// </span><span style="color: green">- Empty string, when all tables contain no rows.
    </span><span style="color: gray">/// &lt;/returns&gt;
    </span><span style="color: blue">public string </span>ToJson(<span style="color: #2b91af">DataSet </span>dataSet)
    {
        <span style="color: blue">if </span>(dataSet == <span style="color: blue">null</span>) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;dataSet&quot;</span>); }

        <span style="color: #2b91af">StringBuilder </span>result = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);
        <span style="color: blue">if </span>(dataSet.Tables.Count &gt; 0)
        {
            result.Append(<span style="color: #a31515">&quot;[&quot;</span>);
            <span style="color: blue">foreach </span>(<span style="color: #2b91af">DataTable </span>table <span style="color: blue">in </span>dataSet.Tables)
            {
                result.Append(ToJson(table));
            }
            result.Append(<span style="color: #a31515">&quot;]&quot;</span>);
        }
        <span style="color: blue">return </span>result.ToString();
    }

    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">Converts a DataTable to a JSON string.
    </span><span style="color: gray">/// &lt;/summary&gt;
    /// &lt;param name=&quot;table&quot;&gt;</span><span style="color: green">The dataset to convert.</span><span style="color: gray">&lt;/param&gt;
    /// &lt;exception cref=&quot;System.ArgumentException&quot;&gt;</span><span style="color: green">Thrown when parameter [table] is null.</span><span style="color: gray">&lt;/exception&gt;
    /// &lt;returns&gt;
    /// </span><span style="color: green">- JSON in the format JSON in the format [[Row0Column0,Row0Column1],[Row1Column0,Row1Column1]]
    </span><span style="color: gray">/// </span><span style="color: green">- Empty string, when datatable contains no rows.
    </span><span style="color: gray">/// &lt;/returns&gt;
    </span><span style="color: blue">public string </span>ToJson(<span style="color: #2b91af">DataTable </span>table)
    {
        <span style="color: blue">if </span>(table == <span style="color: blue">null</span>) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;table&quot;</span>); }

        <span style="color: #2b91af">StringBuilder </span>result = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);
        <span style="color: blue">if </span>(table.Rows.Count &gt; 0)
        {
            result.Append(<span style="color: #a31515">&quot;[&quot;</span>);
            <span style="color: blue">foreach </span>(<span style="color: #2b91af">DataRow </span>row <span style="color: blue">in </span>table.Rows)
            {
                result.Append(ToJson(row));
            }
            result.Append(<span style="color: #a31515">&quot;]&quot;</span>);
        }
        <span style="color: blue">return </span>result.ToString();
    }

    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">Converts a DataRow to a JSON string.
    </span><span style="color: gray">/// &lt;/summary&gt;
    /// &lt;param name=&quot;row&quot;&gt;</span><span style="color: green">The data row to convert.</span><span style="color: gray">&lt;/param&gt;
    /// &lt;exception cref=&quot;System.ArgumentException&quot;&gt;</span><span style="color: green">Thrown when parameter [row] is null.</span><span style="color: gray">&lt;/exception&gt;
    /// &lt;exception cref=&quot;System.ArgumentException&quot;&gt;</span><span style="color: green">Thrown when property [DateTimeFormat] is null, empty or contains only whitespaces.</span><span style="color: gray">&lt;/exception&gt;
    /// &lt;returns&gt;
    /// </span><span style="color: green">- JSON in the format [Row0Column0,Row0Column1].
    </span><span style="color: gray">/// </span><span style="color: green">- Empty string, when datarow contains no columns.
    </span><span style="color: gray">/// &lt;/returns&gt;
    </span><span style="color: blue">public string </span>ToJson(<span style="color: #2b91af">DataRow </span>row)
    {
        <span style="color: blue">if </span>(row == <span style="color: blue">null</span>) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;row&quot;</span>); }
        <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrWhiteSpace(DateTimeFormat)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;DateTimeFormat&quot;</span>); }

        <span style="color: #2b91af">StringBuilder </span>result = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);
        <span style="color: blue">if </span>(row.ItemArray.Count() &gt; 0)
        {
            <span style="color: blue">var </span>serializer = <span style="color: blue">new </span><span style="color: #2b91af">JavaScriptSerializer</span>();
            <span style="color: blue">string </span>json = serializer.Serialize(row.ItemArray);

            <span style="color: green">// Replace Date(...) by a string in the format found in the property [DateTimeFormat].
            </span><span style="color: blue">var </span>matchEvaluator = <span style="color: blue">new </span>MatchEvaluator(ConvertJsonDateToDateString);
            <span style="color: blue">var </span>regex = <span style="color: blue">new </span><span style="color: #2b91af">Regex</span>(<span style="color: #a31515">@&quot;\\/Date\((-?\d+)\)\\/&quot;</span>);
            json = regex.Replace(json, matchEvaluator);

            result.Append(json);
        }
        <span style="color: blue">return </span>result.ToString();
    }

    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">Converts a JSON string to a object array.
    </span><span style="color: gray">/// &lt;/summary&gt;
    /// &lt;param name=&quot;input&quot;&gt;</span><span style="color: green">The input.</span><span style="color: gray">&lt;/param&gt;
    /// &lt;exception cref=&quot;System.ArgumentException&quot;&gt;</span><span style="color: green">Thrown when input is null.</span><span style="color: gray">&lt;/exception&gt;
    /// &lt;returns&gt;&lt;/returns&gt;
    </span><span style="color: blue">public object</span>[] FromJson(<span style="color: blue">string </span>input)
    {
        <span style="color: blue">if </span>(input == <span style="color: blue">null</span>) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;input&quot;</span>); }
        <span style="color: blue">var </span>serializer = <span style="color: blue">new </span><span style="color: #2b91af">JavaScriptSerializer</span>();
        <span style="color: blue">object</span>[] result = serializer.Deserialize(input, <span style="color: blue">typeof</span>(<span style="color: blue">object</span>[])) <span style="color: blue">as object</span>[];

        <span style="color: blue">return </span>result;
    }

    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">Replace JSON dates, like &quot;\/Date(1330740183000)\/&quot; to a string in the format found in the property [DateTimeFormat].
    </span><span style="color: gray">/// &lt;/summary&gt;
    /// &lt;param name=&quot;match&quot;&gt;</span><span style="color: green">When null, throws exception</span><span style="color: gray">&lt;/param&gt;
    /// &lt;exception cref=&quot;ArgumentNullException&quot;&gt;</span><span style="color: green">Throws ArgumentNullException, when property [DateTimeFormat] is null, empty or contains only white spaces.</span><span style="color: gray">&lt;/exception&gt;
    /// &lt;returns&gt;</span><span style="color: green">A string in the format found in the property [DateTimeFormat]</span><span style="color: gray">&lt;/returns&gt;
    </span><span style="color: blue">public string </span>ConvertJsonDateToDateString(<span style="color: #2b91af">Match </span>match)
    {
        <span style="color: blue">if </span>(match == <span style="color: blue">null</span>) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;match&quot;</span>); }
        <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrWhiteSpace(DateTimeFormat)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;DateTimeFormat&quot;</span>); }

        <span style="color: blue">string </span>result = <span style="color: blue">string</span>.Empty;
        <span style="color: #2b91af">DateTime </span>dt = <span style="color: blue">new </span><span style="color: #2b91af">DateTime</span>(1970, 1, 1); <span style="color: green">// Epoch date, used by the JavaScriptSerializer to represent starting point of datetime in JSON.
        </span>dt = dt.AddMilliseconds(<span style="color: blue">long</span>.Parse(match.Groups[1].Value));
        dt = dt.ToLocalTime();
        result = dt.ToString(DateTimeFormat);
        <span style="color: blue">return </span>result;
    }
}</pre>

<p>&#160;</p>

<p>Just an other tip on JSON, if you want to de-serialize a JSON string containing a object with field names, you can use:</p>

<pre class="code"><span style="color: blue">string </span>json = <span style="color: #a31515">@&quot;{Id:1,Barcode:&quot;&quot;WWW12312345678&quot;&quot;}&quot;</span>;
<span style="color: blue">var </span>serializer = <span style="color: blue">new </span><span style="color: #2b91af">JavaScriptSerializer</span>();
<span style="color: blue">var </span>dict = serializer.Deserialize&lt;<span style="color: #2b91af">Dictionary</span>&lt;<span style="color: blue">string</span>, <span style="color: blue">string</span>&gt;&gt;(json);
<span style="color: #2b91af">Console</span>.WriteLine(dict[<span style="color: #a31515">&quot;Barcode&quot;</span>]);</pre>