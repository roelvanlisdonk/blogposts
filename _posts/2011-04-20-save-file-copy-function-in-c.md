---
ID: 1989
post_title: 'Save file copy function in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/04/20/save-file-copy-function-in-c/
published: true
post_date: 2011-04-20 16:56:02
---
<p>If you want to copy a file to a folder, which is polled by a import service, you want the import service to start processing the file, when it is fully copied to the folder. This can be done with the following code:</p>  <p>&#160;</p>   <pre class="code"><span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">Copy a file to a destinationfolder, with the fileextension renamed to [tempFileExtension]
</span><span style="color: gray">/// </span><span style="color: green">After copy, rename the destination file to it's original file extension
</span><span style="color: gray">/// </span><span style="color: green">This methode can be used in scenario's, where a service is polling a folder and you don't want the service to start processing the file, when it is not fully copied yet
</span><span style="color: gray">/// &lt;/summary&gt;
/// &lt;param name=&quot;sourceFolder&quot;&gt;</span><span style="color: green">Can't be empty</span><span style="color: gray">&lt;/param&gt;
/// &lt;param name=&quot;destinationFolder&quot;&gt;</span><span style="color: green">Can't be empty</span><span style="color: gray">&lt;/param&gt;
/// &lt;param name=&quot;fileName&quot;&gt;</span><span style="color: green">Can't be empty. Should be the name of the file, including the file extension</span><span style="color: gray">&lt;/param&gt;
/// &lt;param name=&quot;tempFileExtension&quot;&gt;</span><span style="color: green">Can't be empty</span><span style="color: gray">&lt;/param&gt;
</span><span style="color: blue">public static void </span>SaveFileCopy(<span style="color: blue">string </span>sourceFolder, <span style="color: blue">string </span>destinationFolder, <span style="color: blue">string </span>fileName, <span style="color: blue">string </span>tempFileExtension)
{
    <span style="color: green">// Determine source file path
    </span><span style="color: blue">string </span>sourceFile = <span style="color: #2b91af">Path</span>.Combine(sourceFolder, fileName);

    <span style="color: green">// Determine temp destination file path
    </span><span style="color: blue">string </span>tempDestinationFile = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}{1}&quot;</span>, <span style="color: #2b91af">Path</span>.Combine(destinationFolder, fileName), tempFileExtension);

    <span style="color: green">// Set temp destination file to [not-readonly]
    </span><span style="color: blue">if </span>(<span style="color: #2b91af">File</span>.Exists(tempDestinationFile))
    {
        <span style="color: #2b91af">File</span>.SetAttributes(tempDestinationFile, <span style="color: #2b91af">FileAttributes</span>.Normal);
    }

    <span style="color: green">// Copy the file as temp file extension
    </span><span style="color: #2b91af">File</span>.Copy(sourceFile, tempDestinationFile, <span style="color: blue">true</span>);

    <span style="color: green">// Determine destination file path
    </span><span style="color: blue">string </span>destinationFile = <span style="color: #2b91af">Path</span>.Combine(destinationFolder, fileName);

    <span style="color: green">// Set destination file to [not-readonly]
    </span><span style="color: blue">if </span>(<span style="color: #2b91af">File</span>.Exists(destinationFile))
    {
        <span style="color: #2b91af">File</span>.SetAttributes(destinationFile, <span style="color: #2b91af">FileAttributes</span>.Normal);
    }

    <span style="color: green">// Delete the destination file if it exists
    </span><span style="color: blue">if </span>(<span style="color: #2b91af">File</span>.Exists(destinationFile)) { <span style="color: #2b91af">File</span>.Delete(destinationFile); }

    <span style="color: green">// Rename the file to it's original file extension
    </span><span style="color: #2b91af">File</span>.Move(tempDestinationFile, destinationFile);
}</pre>