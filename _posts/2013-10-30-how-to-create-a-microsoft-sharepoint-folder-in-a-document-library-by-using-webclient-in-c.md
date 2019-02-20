---
ID: 3521
post_title: 'How to create a Microsoft SharePoint folder in a document library, by using WebClient in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/10/30/how-to-create-a-microsoft-sharepoint-folder-in-a-document-library-by-using-webclient-in-c/
published: true
post_date: 2013-10-30 09:16:32
---
<p>&#160;</p>  <p>If you want to create a folder in a document library, by using WebClient in C#, you can use the following code:</p>  <p>&#160;</p>   <pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Net;

    [</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">RliResearch
    </span><span style="background: white; color: black">{
        [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">CreateSharePointFolderInDocumentLibrary()
        {
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">folderToCreateUri = </span><span style="background: white; color: #a31515">&quot;https://1.1.1.1/sites/mysite/Shared%20Documents/FolderIWantToCreate&quot;</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">client = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">WebClient</span><span style="background: white; color: black">())
            {
                client.Credentials = </span><span style="background: white; color: #2b91af">CredentialCache</span><span style="background: white; color: black">.DefaultCredentials;
                client.UploadString(folderToCreateUri, </span><span style="background: white; color: #a31515">&quot;MKCOL&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;&quot;</span><span style="background: white; color: black">);
            }
        }
    }
}
</span></pre>


<p>Note: The folder you want to create the folder in, must exist. In other words: create subfolder hierarchy one at a time.</p>

<p>To create the folder hierarchy:</p>

<p>Shared Documents</p>

<p>&#160;&#160;&#160;&#160; SubLevel1</p>

<p>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; SubLevel2</p>

<p>&#160;</p>

<pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Net;

    [</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">RliResearch
    </span><span style="background: white; color: black">{
        [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">CreateSharePointFolderInDocumentLibrary()
        {
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">sublevel1 = </span><span style="background: white; color: #a31515">&quot;https://1.1.1.1/sites/mysite/Shared%20Documents/SubLevel1&quot;</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">client = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">WebClient</span><span style="background: white; color: black">())
            {
                client.Credentials = </span><span style="background: white; color: #2b91af">CredentialCache</span><span style="background: white; color: black">.DefaultCredentials;
                client.UploadString(sublevel1, </span><span style="background: white; color: #a31515">&quot;MKCOL&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;&quot;</span><span style="background: white; color: black">);
            }

            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">sublevel2 = </span><span style="background: white; color: #a31515">&quot;https://1.1.1.1/sites/mysite/Shared%20Documents/SubLevel1/SubLevel2&quot;</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">client = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">WebClient</span><span style="background: white; color: black">())
            {
                client.Credentials = </span><span style="background: white; color: #2b91af">CredentialCache</span><span style="background: white; color: black">.DefaultCredentials;
                client.UploadString(sublevel2, </span><span style="background: white; color: #a31515">&quot;MKCOL&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;&quot;</span><span style="background: white; color: black">);
            }
        }
    }
}
</span></pre>