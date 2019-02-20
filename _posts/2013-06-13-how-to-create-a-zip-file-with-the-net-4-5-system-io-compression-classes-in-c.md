---
ID: 3234
post_title: 'How to create a Zip file with the .NET 4.5 System.IO.Compression classes in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/06/13/how-to-create-a-zip-file-with-the-net-4-5-system-io-compression-classes-in-c/
published: true
post_date: 2013-06-13 21:25:25
---
<p>If you want to create a zip file in C# with the OOB BCL, in C# you can use the following code:</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">public void </span><span style="background: white; color: black">CreateZipFile()
{
    </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">zipPath = </span><span style="background: white; color: #a31515">@&quot;C:\Test.zip&quot;</span><span style="background: white; color: black">;
    </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">entryName = </span><span style="background: white; color: #a31515">&quot;Readme.txt&quot;</span><span style="background: white; color: black">;
    </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">content = </span><span style="background: white; color: #a31515">&quot;Hello world!&quot;</span><span style="background: white; color: black">;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">zipToOpen = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">System.IO.</span><span style="background: white; color: #2b91af">FileStream</span><span style="background: white; color: black">(zipPath, System.IO.</span><span style="background: white; color: #2b91af">FileMode</span><span style="background: white; color: black">.CreateNew))
    {
        </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">archive = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">System.IO.Compression.</span><span style="background: white; color: #2b91af">ZipArchive</span><span style="background: white; color: black">(zipToOpen, System.IO.Compression.</span><span style="background: white; color: #2b91af">ZipArchiveMode</span><span style="background: white; color: black">.Create))
        {
            System.IO.Compression.</span><span style="background: white; color: #2b91af">ZipArchiveEntry </span><span style="background: white; color: black">readmeEntry = archive.CreateEntry(entryName);
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">writer = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">System.IO.</span><span style="background: white; color: #2b91af">StreamWriter</span><span style="background: white; color: black">(readmeEntry.Open()))
            {
                writer.Write(content);
            }
        }
    }
}</span></pre>