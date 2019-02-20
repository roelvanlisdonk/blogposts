---
ID: 3610
post_title: 'How to convert a string to a stream, without using encoding in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/12/13/how-to-convert-a-string-to-a-stream-without-using-encoding-in-c/
published: true
post_date: 2013-12-13 15:23:43
---
<p>If you want to convert a string to a stream, without using encoding. You can use the following string extension:</p>  <p>&#160;</p>  <p><strong>usage</strong></p>  <pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">PTB.Cs.Test.Research
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">PTB.Cs.Extensions;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.IO;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Xunit;

    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">RliTester
    </span><span style="background: white; color: black">{
        
        [</span><span style="background: white; color: #2b91af">Fact</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Test()
        {
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">subject = </span><span style="background: white; color: #a31515">&quot;Some text.&quot;</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">long </span><span style="background: white; color: black">expected = 10;
            </span><span style="background: white; color: blue">long </span><span style="background: white; color: black">actual = 0;

            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">Stream </span><span style="background: white; color: black">stream = subject.ToStream())
            {
                actual = stream.Length;
            }    
            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.Equal(expected, actual);
        }
    }
}

</span></pre>
<strong>Code</strong>

<pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Extensions
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.IO;

    </span><span style="background: white; color: blue">public static class </span><span style="background: white; color: #2b91af">StringExtensions
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Convert a string to a stream, without using encoding.
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">Don't forget to dispose the &quot;result&quot; stream in the calling method.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;subject&quot;&gt;</span><span style="background: white; color: green">The string to convert.</span><span style="background: white; color: gray">&lt;/param&gt;
        /// &lt;returns&gt;</span><span style="background: white; color: green">A stream with position set to 0.</span><span style="background: white; color: gray">&lt;/returns&gt;
        </span><span style="background: white; color: blue">public static </span><span style="background: white; color: #2b91af">Stream </span><span style="background: white; color: black">ToStream(</span><span style="background: white; color: blue">this string </span><span style="background: white; color: black">subject)
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">result = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">MemoryStream</span><span style="background: white; color: black">();

            </span><span style="background: white; color: blue">using</span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">stream = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">MemoryStream</span><span style="background: white; color: black">())
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">writer = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">StreamWriter</span><span style="background: white; color: black">(stream))
            {
                writer.Write(subject);
                writer.Flush();
                stream.Position = 0;
                stream.CopyTo(result);
                result.Position = 0;
            }
            
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">result;
        }
    }
}</span></pre>