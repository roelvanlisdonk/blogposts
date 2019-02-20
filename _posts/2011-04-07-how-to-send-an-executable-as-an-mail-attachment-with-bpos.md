---
ID: 1948
post_title: >
  How to send an executable as an E-mail
  attachment with BPOS
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/04/07/how-to-send-an-executable-as-an-mail-attachment-with-bpos/
published: true
post_date: 2011-04-07 11:40:43
---
Out of the box sending executables as attachments with BPOS is not possible. BPOS will replace the executable with a *.txt file that contains the text:

<span style="font-size: xx-small;"><em>FILE QUARANTINED</em></span>

<span style="font-size: xx-small;"><em>Microsoft Online has removed winmail.dat-&gt;Unnamed Attachment-&gt;YoureApplication.exe since it
was found to match the FILE FILTER= unnamed: *.exe file filter.</em></span>

Even if you zip or rar the file and rename the file extension, BPOS will replace the executable in the zip or RAR file with the txt file.

To prevent BPOS from removing the executable you can ask you administrator to edit the FILE FILTER rule or you can follow the steps below:
<ul>
	<li>Zip the executable file</li>
	<li>Open the zip file with a hexeditor (I use Notepad++ with the HexEditor.dll plugin)</li>
	<li>Change the first 2 letters "PK" to some other letters, for example "LL"</li>
	<li>Save the zip file</li>
	<li>Send it to the customer</li>
	<li>Customer must open the zip file with a hexeditor</li>
	<li>Change the first 2 letters "LL" back to "PK" and save the zip file</li>
	<li>Then the customer can extract the zip file and use the "YoureApplication.exe"</li>
</ul>