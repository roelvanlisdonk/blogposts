---
ID: 463
post_title: >
  Bulk Insert Error Operating system error
  code 1265
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/25/bulk-insert-error-operating-system-error-code-1265/
published: true
post_date: 2009-05-25 09:01:52
---
<p>When you get the error:    <br />Cannot bulk load because the file <a href="file://server01/NetworkShare/xxx.txt">\\SERVER01\NetworkShare\xxx.txt</a>    <br />could not be opened. Operating system error code 1265(The system detected a possible attempt to compromise security. Please ensure that you can contact the server that authenticated you.).     <br />Make sure the credentials of the Windows Service which calls the stored procedure that executes the bulk insert statement, are correct. In our case the password was changed, so the service was started with a password different from the correct and current password.</p>