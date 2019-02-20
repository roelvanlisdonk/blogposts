---
ID: 4709
post_title: >
  Convert SourceGear Vault Standard v3.1.9
  to Git including all history
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/12/17/convert-sourcegear-vault-standard-v3-1-9-to-git-including-all-history/
published: true
post_date: 2015-12-17 15:44:01
---
To convert files from a SoureGear Vault Standard v3.1.9 to Git including all history I went on a journey and in this blog post I will describe the journey steps.

Note: this blog post will probably contain unnecessary steps, but non the less it describes the steps how I successfully converted all files found in a SourceGear Vault Standard v3.1.9 server to Git, including all history.

&nbsp;
<h1>Steps</h1>
&nbsp;
<h2>Notes</h2>
<ul>
	<li>The SourceGear Vault Standard v3.1.9 was installed on a Microsoft Windows 2003 32bit Server.</li>
	<li>On the server was a Microsoft SQL Server 2005 32 bit installation.</li>
	<li>During the upgrade I switched to a Windows 10 (64 bit) Hyper-V machine.</li>
	<li>To prevent “multi user” sql connection problems, make sure you stop the vault service with a iisreset /stop, before installation.</li>
	<li>All developers should checkin their files on the SourceGear Vault Standard v3.1.9 server.</li>
	<li>Verify that no files are checked out with the Vault Standard v3.1.9 admin tool.</li>
	<li>If you are using SQL Server 2005 make sure that the database sgvault is in SQL Server 2005 compatibility modus</li>
</ul>
&nbsp;

&nbsp;
<h2>Steps on the Microsoft Windows 2003 32bit Server</h2>
&nbsp;
<ul>
	<li>For the conversion, I added the SourceGear Vault Service IIS <strong>application pool user</strong>, to the <strong>local administrator group</strong>.</li>
	<li>Our Vault Service connects to SQL Server by using windows authentication. I added the sgvaultuser, Network Service and the locale user that was executing the setups to the SQL Server <strong>sysadmin</strong> group for the conversion.</li>
</ul>
<a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2015/12/image-6.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px; display: inline; padding-right: 0px; border: 0px;" title="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2015/12/image_thumb-6.png" alt="image" width="244" height="172" border="0" /></a>
<ul>
	<li>At the end of the following installs <strong>don’t</strong> install the Vault Client</li>
	<li>Download and install <a title="http://download-us.sourcegear.com/Vault/3.5.3.5169/VaultServer_3_5_3.msi" href="http://download-us.sourcegear.com/Vault/3.5.3.5169/VaultServer_3_5_3.msi">http://download-us.sourcegear.com/Vault/3.5.3.5169/VaultServer_3_5_3.msi</a>
<ul>
	<li>Note I had troubles installing VaultServer 3.5.3, when using sql authentication, i got a Error Code = –1001 and also an Error Code = –1280, this was resolved by using windows authentication for this installation.</li>
	<li>I also neede to manualy set the database “Restrict Access” back to Multiple</li>
	<li><a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2015/12/image-5.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2015/12/image_thumb-5.png" alt="image" width="244" height="137" border="0" /></a></li>
</ul>
</li>
	<li>
<div align="left">Download and install <a title="http://download-us.sourcegear.com/Vault/4.0.6.15954/VaultServer_4_0_6_15954.msi" href="http://download-us.sourcegear.com/Vault/4.0.6.15954/VaultServer_4_0_6_15954.msi">http://download-us.sourcegear.com/Vault/4.0.6.15954/VaultServer_4_0_6_15954.msi</a></div>
<ul>
	<li>
<div align="left">If this upgrade fails on setting foreignkeys for table tblcheckoutlistitems, then check <a href="http://http://kb.sourcegear.com/FortressHelp/viewtopic.php?f=5&amp;t=9826">this</a></div></li>
</ul>
</li>
	<li>
<div align="left">Download and install <a title="http://download-us.sourcegear.com/Vault/4.1.4.18402/VaultServer_4_1_4_18402.msi" href="http://download-us.sourcegear.com/Vault/4.1.4.18402/VaultServer_4_1_4_18402.msi">http://download-us.sourcegear.com/Vault/4.1.4.18402/VaultServer_4_1_4_18402.msi</a></div></li>
	<li>
<div align="left">Download and install WIC <a title="https://www.microsoft.com/en-us/download/confirmation.aspx?id=32" href="https://www.microsoft.com/en-us/download/confirmation.aspx?id=32">https://www.microsoft.com/en-us/download/confirmation.aspx?id=32</a></div></li>
	<li>
<div align="left">Download and install .net 3.5 <a title="http://download.microsoft.com/download/2/0/e/20e90413-712f-438c-988e-fdaa79a8ac3d/dotnetfx35.exe" href="http://download.microsoft.com/download/2/0/e/20e90413-712f-438c-988e-fdaa79a8ac3d/dotnetfx35.exe">http://download.microsoft.com/download/2/0/e/20e90413-712f-438c-988e-fdaa79a8ac3d/dotnetfx35.exe</a></div></li>
	<li>
<div align="left">Download and Install .NET 4.0 <a title="https://www.microsoft.com/en-us/download/confirmation.aspx?id=17718" href="https://www.microsoft.com/en-us/download/confirmation.aspx?id=17718">https://www.microsoft.com/en-us/download/confirmation.aspx?id=17718</a></div>
<ul>
	<li>
<div align="left">Note: this takes a while on Windows 2003 server.</div></li>
</ul>
<!--EndFragment--></li>
	<li>
<div align="left">Download and install <a title="http://download-us.sourcegear.com/Vault/5.0.4.18845/VaultServer_5_0_4_18845.msi" href="http://download-us.sourcegear.com/Vault/5.0.4.18845/VaultServer_5_0_4_18845.msi">http://download-us.sourcegear.com/Vault/5.0.4.18845/VaultServer_5_0_4_18845.msi</a></div></li>
	<li>
<div align="left">Download and install <a title="http://download-us.sourcegear.com/Vault/5.1.2.19281/VaultServer_5_1_2_19281.msi" href="http://download-us.sourcegear.com/Vault/5.1.2.19281/VaultServer_5_1_2_19281.msi">http://download-us.sourcegear.com/Vault/5.1.2.19281/VaultServer_5_1_2_19281.msi</a></div></li>
	<li>
<div align="left">Download and install <a title="http://download-us.sourcegear.com/Vault/6.1.0.531/VaultServer_6_1_0_531.msi" href="http://download-us.sourcegear.com/Vault/6.1.0.531/VaultServer_6_1_0_531.msi">http://download-us.sourcegear.com/Vault/6.1.0.531/VaultServer_6_1_0_531.msi</a></div></li>
	<li>
<div align="left">Backup the SQL Server 2005 databases: sgmaster, sgnotify, sgvault, sgvaultindex</div></li>
</ul>
&nbsp;
<h2>Steps on the Microsoft Windows 10 64bit Hyper-V virutal machine</h2>
The following steps were executed on an empty Microsoft Windows 10 (64 bit) Hyper-V virtual machine.
<ul>
	<li>
<div align="left">Turn the Windows IIS feature on (including all sub features)</div></li>
	<li>
<div align="left">Install SQL Server 2014 (64 bit)</div></li>
	<li>
<div align="left">Create databases on SQL Server 2014: sgmaster, sgnotify, sgvault, sgvaultindex</div></li>
	<li>
<div align="left">Restore the databases on SQL Server 2014 from the SQL Server 2005 backups: sgmaster, sgnotify, sgvault, sgvaultindex</div></li>
	<li>
<div align="left">Set compatibility modus to SQL Server 2014 for the SQL Server 2014 databases: sgmaster, sgnotify, sgvault, sgvaultindex</div></li>
	<li>
<div align="left">Execute SQL “login / user” correction script, found at: <a title="http://support.sourcegear.com/viewtopic.php?t=924" href="http://support.sourcegear.com/viewtopic.php?t=924">http://support.sourcegear.com/viewtopic.php?t=924</a></div></li>
	<li>
<div align="left">Download and install <a title="http://download.sourcegear.com/Vault/9.0.0.452/VaultServer64_9_0_0_452.msi" href="http://download.sourcegear.com/Vault/9.0.0.452/VaultServer64_9_0_0_452.msi">http://download.sourcegear.com/Vault/9.0.0.452/VaultServer64_9_0_0_452.msi</a></div></li>
	<li>
<div align="left">Install the Vault Client</div></li>
	<li>
<div align="left">Verify we have a working Vault Standard v9.0.0 installation.</div></li>
</ul>
<p align="left"></p>

<h3 align="left">Git</h3>
<ul>
	<li>
<div align="left">Install Git <a title="https://git-scm.com/downloads" href="https://git-scm.com/downloads">https://git-scm.com/downloads</a> in my case it was v2.6.4 Git for Windows.</div></li>
	<li>During installation make sure, you choose: “Run Git and included Unix tools from the Windows Command Prompt”.</li>
	<li>Intialize Git, set username and email</li>
	<li>Create a folder "C:\Projects\Git\MyRepo"</li>
	<li>Create a GIT repository inside "C:\Projects\Git\MyRepo" by executing: git init.</li>
	<li>
<div align="left">Commit one file (e.g. an .ignore file) to the MyRepo master with a initial commit.</div></li>
	<li>
<div align="left"><span style="color: #ff0000;">IMPORTANT, do a GET of all Vault files</span> to this <span style="color: #ff0000;">MyRepo</span> folder, <strong><span style="color: #ff0000;">making all files writable</span></strong></div></li>
</ul>
<p align="left"></p>

<ul><!--EndFragment--></ul>
<p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/12/image-1.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/12/image_thumb-1.png" alt="image" width="444" height="380" border="0" /></a></p>
<p align="left"></p>
<p align="left"></p>

<h3 align="left">Vaut2Git</h3>
<ul>
	<li>
<div align="left">Install Visual Studio 2015 community edition</div></li>
	<li>
<div align="left">Download the vault2git tooling <a title="https://github.com/AndreyNikiforov/vault2git/archive/master.zip" href="https://github.com/AndreyNikiforov/vault2git/archive/master.zip">https://github.com/AndreyNikiforov/vault2git/archive/master.zip</a></div></li>
	<li>
<div align="left">Extract the zip file and open the solution with Visual Studio 2015 community edition.</div></li>
	<li>
<div align="left">Download the Client API belonging to Vault v9.0.0 <a title="http://download.sourcegear.com/VaultPro/9.0.0.30452/VaultProClientAPI_9_0_0_30452.zip" href="http://download.sourcegear.com/VaultPro/9.0.0.30452/VaultProClientAPI_9_0_0_30452.zip">http://download.sourcegear.com/VaultPro/9.0.0.30452/VaultProClientAPI_9_0_0_30452.zip</a></div></li>
	<li>
<div align="left">Extract the files from the Client API zip</div></li>
	<li>
<div align="left">Copy the folder to the <strong>Vault2GitLib/libs</strong> folder and adjust the references</div></li>
</ul>
<p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/12/image-2.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/12/image_thumb-2.png" alt="image" width="356" height="604" border="0" /></a></p>

<ul>
	<li>
<div align="left">Build the solution in release modus.</div></li>
</ul>
<p align="left"></p>

<h2 align="left">Now the really import part is adjusting the App.config file</h2>
<p align="left"></p>
<p align="left"><strong>Vault.Server</strong></p>
<p align="left">The servername, because I am running the vault2git tool on the vault server this is localhost.</p>
<p align="left"><strong>Vault.User</strong></p>
<p align="left">The vault user name used to login to the SourceGear Vault.</p>
<p align="left"><strong>Vault.Password</strong></p>
<p align="left">The vault user password used to login to the SourceGear Vault.</p>
<p align="left"><strong>Vault.Repo</strong></p>
<p align="left">The Vault repository name, to get the files from</p>
<p align="left"><strong>Git.DomainName</strong></p>
<p align="left">This is the part that will be added to each Vault username to create a Git user email from a Vault username.</p>
<p align="left"><strong>Convertor.WorkingFolder</strong></p>
<p align="left">This folder must be the Git repository root folder.</p>
<p align="left">This folder should contain a “.git” folder, before the vault2git is run.</p>
<p align="left"><strong>Convertor.GitCmd</strong></p>
<p align="left">The path to the git.exe to use.</p>
<p align="left"><strong>Convertor.Paths</strong></p>
<p align="left">At first this is a “;” seperated list of conversions.</p>
<p align="left">Each conversion is a “~” seperated key value pair.</p>
<p align="left">The first part of the conversion is the path in the Vault (in this case the root of the vault “$”).</p>
<p align="left">The second part of the conversion is the Git branch (in this case “master”)</p>
<p align="left">In this case only one conversion is done, namely converting all the files from a Vault respository to a Git repository branch called master.</p>
<p align="left"></p>
<p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/12/image-3.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/12/image_thumb-3.png" alt="image" width="580" height="218" border="0" /></a></p>
<p align="left"></p>
<p align="left"></p>
<p align="left"><strong>NOW RUN THE vault2git.exe</strong></p>
<p align="left">It should convert all files from vault to git</p>
<p align="left">note that this takes a long time.</p>
<p align="left"><strong>In my case 7MB of Vault Source files took 23 minutes to convert!!</strong></p>
<p align="left"></p>

<h2 align="left">Bitbucket</h2>
<p align="left">Now that we have a locale Git repository containing all Vault Sources and history, we can push this Git respository to a remote Git respository (in our case a Bitbucket service).</p>

<ul>
	<li>
<div align="left">Create a Git repository in bitbucket.</div></li>
	<li>
<div align="left">Add users to the Git repository</div></li>
	<li>
<div align="left">Adjust the client_max_body_size (we set it to 0) in the files:</div>
<ul>
	<li>
<div align="left">/etc/nginx/nginx.conf (Use sudo vim, else the file will be read-only)</div></li>
	<li>
<div align="left">/etc/nginx/sites-available/bitbucket-cache</div></li>
	<li>
<div align="left">This is to allow large commits</div></li>
</ul>
</li>
	<li>
<div align="left">Adjust postBuffer: git config --global http.postBuffer 1048576000</div>
<ul>
	<li>
<div align="left">This is to allow large commits (&lt;= 1GB)</div></li>
</ul>
</li>
</ul>
<p align="left"></p>
&nbsp;
<h2>Some additional information and Notes</h2>
&nbsp;

<strong>Moving vault databases</strong>

<a href="http://support.sourcegear.com/viewtopic.php?t=924">http://support.sourcegear.com/viewtopic.php?t=924</a>

<strong>Vault upgrade guide</strong>

<a href="http://kb.sourcegear.com/VaultHelp/viewtopic.php?f=13&amp;t=11648">http://kb.sourcegear.com/VaultHelp/viewtopic.php?f=13&amp;t=11648</a>

<strong>Vault compatibility chart</strong>

<a href="http://www.sourcegear.com/vault/documentation/compatibility_chart.html">http://www.sourcegear.com/vault/documentation/compatibility_chart.html</a>
<p align="left"><strong>SQL “login / user” correction script</strong></p>
USE [master]
IF ( NOT EXISTS (SELECT sid FROM syslogins WHERE name = 'sgvaultuser') )
CREATE LOGIN sgvaultuser WITH PASSWORD = N'VAULTS_ADMIN_PWD', DEFAULT_DATABASE = sgvault, CHECK_POLICY = OFF;
GO
-- next access should be granted in the vault database
USE [sgvault]
EXEC sp_grantdbaccess N'sgvaultuser'
EXEC sp_addrolemember N'db_owner', N'sgvaultuser'
GO
-- The following is ONLY for Fortress and VaultPro:
USE [sgdragnet]
EXEC sp_grantdbaccess N'sgvaultuser'
EXEC sp_addrolemember N'db_owner', N'sgvaultuser'
GO
-- The following is for Vault 4.x and above or Fortress and VaultPro:
USE [sgmaster]
EXEC sp_grantdbaccess N'sgvaultuser'
EXEC sp_addrolemember N'db_owner', N'sgvaultuser'
GO

&nbsp;

<strong>Rollback</strong>

In my case, something went wrong and I had to rollback from 4.0.6 to 3.1.9.

If you have to restore a old database, make sure you first remove all sofware.

Remove alle databases.

Create a new sgvault database.

Restore the backup to this new sgvault database.