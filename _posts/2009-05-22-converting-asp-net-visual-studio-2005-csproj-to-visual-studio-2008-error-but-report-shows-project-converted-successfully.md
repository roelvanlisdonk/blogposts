---
ID: 451
post_title: >
  Converting ASP .NET Visual Studio 2005
  .csproj to Visual Studio 2008 error, but
  report shows Project converted
  successfully
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/converting-asp-net-visual-studio-2005-csproj-to-visual-studio-2008-error-but-report-shows-project-converted-successfully/
published: true
post_date: 2009-05-22 14:54:45
---
<p>When you convert an ASP .NET Visual Studio 2005 project file to an ASP .NET visual studio 2008 project and you get an error: The project file cannot be converted, see error report. But the error report contains only the message Project converted successfully. You should check if you&#8217;re website exists. In my case I used an hostheader in mine ASP .NET project and on mine new VMWare image that hostheader did not exist. That caused the error.</p>