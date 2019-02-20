---
ID: 362
post_title: >
  System.OutOfMemoryException on SSIS
  Script Task
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/04/21/systemoutofmemoryexception-on-ssis-script-task/
published: true
post_date: 2009-04-21 12:17:43
---
<p>I created a SSIS package with a script task in it. The script task created a XML file, but consumed more then 256MB of memory. The default value for the MemToLeave setting.<br /><br />MemToLeave is virtual address space (VAS) that’s left un-used when SQL Server starts so that external components called by SQL Server are saved some address space. So in order for these technologies, .NET CLR and SSIS, to operate<br />see <a title="http://www.johnsansom.com/index.php/2009/03/sql-server-memory-configuration-determining-memtoleave-settings/" href="http://www.johnsansom.com/index.php/2009/03/sql-server-memory-configuration-determining-memtoleave-settings/">http://www.johnsansom.com/index.php/2009/03/sql-server-memory-configuration-determining-memtoleave-settings/</a><br /><br /></p> <h3>Error</h3><br /> <p><strong></strong>Event Type:&nbsp;&nbsp;&nbsp; Error<br />Event Source:&nbsp;&nbsp;&nbsp; SSIS Package CDS Rapportage<br />Event Category:&nbsp;&nbsp;&nbsp; None<br />Event ID:&nbsp;&nbsp;&nbsp; 3<br />Date:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 4/21/2009<br />Time:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 12:59:29 PM<br />User:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; N/A<br />Computer:&nbsp;&nbsp;&nbsp; NLPRC173N59<br />Description:<br />Unexpected exception Exception.Message[Exception of type 'System.OutOfMemoryException' was thrown.] </p> <p>For more information, see Help and Support Center at http://go.microsoft.com/fwlink/events.asp. <p>&nbsp;</p> <h3>Solution</h3> <p><strong></strong><br />Setting the MemToLeave to 512MB solved the problem.</p>