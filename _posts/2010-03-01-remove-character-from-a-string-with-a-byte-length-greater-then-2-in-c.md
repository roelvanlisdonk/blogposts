---
ID: 1045
post_title: 'Remove character from a string with a byte length greater then 2 in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/01/remove-character-from-a-string-with-a-byte-length-greater-then-2-in-c/
published: true
post_date: 2010-03-01 11:44:07
---
<p>Some application can’t work with characters larger then 2 bytes. You can replace these character by a question mark ‘?’ with the following code:</p>  <pre class="code"><span style="color: gray">        /// &lt;summary&gt;
        /// </span><span style="color: green">Replace all characters with more then 2 bytes by a &quot;?&quot; character
        </span><span style="color: gray">/// </span><span style="color: green">Trim start and end
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;input&quot;&gt;&lt;/param&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color: blue">public static string </span>Replace2BytesOrMoreCharactersAndTrim(<span style="color: blue">string </span>input)
        {
            <span style="color: blue">if</span>(<span style="color: blue">string</span>.IsNullOrEmpty(input))
            {
                <span style="color: blue">return string</span>.Empty;
            }

            <span style="color: green">// Loop characters in input string
            </span><span style="color: blue">char</span>[] characters = input.ToCharArray();
            <span style="color: #2b91af">StringBuilder </span>resultStrinBuilder = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);
            <span style="color: blue">foreach </span>(<span style="color: blue">char </span>character <span style="color: blue">in </span>characters)
            {
                <span style="color: green">// Get utf-8 bytes of character
                </span><span style="color: blue">byte</span>[] characterInBytes = <span style="color: #2b91af">Encoding</span>.UTF8.GetBytes(<span style="color: blue">new char</span>[] { character });

                <span style="color: blue">if </span>(characterInBytes.Length &gt; 2)
                {
                    <span style="color: green">// Replace character by &quot;?&quot; for character with more then 2 bytes
                    </span>resultStrinBuilder.Append(<span style="color: #a31515">&quot;?&quot;</span>);
                }
                <span style="color: blue">else
                </span>{
                    <span style="color: green">// Keep original character
                    </span>resultStrinBuilder.Append(character);
                }
            }

            <span style="color: green">// Remove start en trailing white spaces.
            </span><span style="color: blue">string </span>result = resultStrinBuilder.ToString().Trim();

            <span style="color: green">// Converting to UTF-8 creates a bom, remove the bom</span></pre>

<pre class="code"><span style="color: green">            </span>result = result.TrimStart(<span style="color: #a31515">'?'</span>);

            <span style="color: blue">return </span>result;
        }</pre>
<a href="http://11011.net/software/vspaste"></a>