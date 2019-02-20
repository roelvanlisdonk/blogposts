---
ID: 1228
post_title: 'How to create a JournalItem from a C# Outlook 2010 Add-in'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/04/10/how-to-create-a-journalitem-from-a-c-outlook-2010-add-in/
published: true
post_date: 2010-04-10 12:34:47
---
<p>If you want to create a JournalItem from C#, you van use the following code:   <br />    <br /><strong>Code</strong></p>  <pre class="code"><span style="color: green">// Get the default journal folder
</span><span style="color: #2b91af">MAPIFolder </span>jounalFolder = <span style="color: #2b91af">Globals</span>.ThisAddIn.Application.Session.GetDefaultFolder(<span style="color: #2b91af">OlDefaultFolders</span>.olFolderJournal);<br />            <br /><span style="color: green">// Create a new journal item
</span><span style="color: #2b91af">JournalItem </span>journalItem = jounalFolder.Items.Add(<span style="color: #2b91af">OlItemType</span>.olJournalItem);<br />            <br /><span style="color: green">// Change some values of the new journal item
</span>journalItem.Subject = <span style="color: #a31515">&quot;This is a new JournalItem&quot;</span>;
journalItem.Duration = 60; <span style="color: green">// 60 minutes
</span>journalItem.Start = <span style="color: #2b91af">DateTime</span>.Now;
journalItem.Categories = <span style="color: #a31515">&quot;ADA&quot;</span>;<br />journalItem.Type = <span style="color: #a31515">&quot;Task&quot;</span>; <span style="color: green">// Default is Phone Call </span>

<span style="color: green">// Save the new journal item
</span>journalItem.Save();</pre>
<a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>

<p><strong>Result</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image18.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image_thumb18.png" width="784" height="391" /></a> </p>

<p>
  <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image19.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image_thumb19.png" width="784" height="277" /></a> 

  <br /></p>

<p>&#160;</p>

<p></p>

<p><strong>Note</strong></p>

<p>The code can be used to create Mails, Task, Contacts, Appointments etc. Just change <span style="color: #2b91af">OlDefaultFolders</span>.olFolderJournal and <span style="color: #2b91af">OlItemType</span>.olJournalItem to the correct types.</p>