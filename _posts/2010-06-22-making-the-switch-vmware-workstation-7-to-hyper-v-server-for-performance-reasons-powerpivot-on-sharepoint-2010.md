---
ID: 1532
post_title: 'Making the switch: VMWare Workstation 7 to Hyper-V server for performance reasons (PowerPivot on SharePoint 2010)'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/22/making-the-switch-vmware-workstation-7-to-hyper-v-server-for-performance-reasons-powerpivot-on-sharepoint-2010/
published: true
post_date: 2010-06-22 21:16:40
---
<p>&#160;</p>  <p><strong>History</strong></p>  <p align="left">Back in 2002 I was working with a company which produced a CAD application written in VB6. The product was released in several languages. For each language we had a Microsoft Windows NT 4 workstation with the corresponding language package. I quickly realized that managing these workstations was difficult. So I started to look at virtualization, but it was not until 2003 with new hardware and an other company when I decided to take a look at VMware Workstation version 4.0. This was great I could run all Microsoft Windows languages and different versions on 1 system! Then in 2004 Microsoft released Microsoft Virtual Server 2005 I took a look at the product but soon realized that it could not compete with VMware Workstation and I kept on using VMware Workstation. This worked great for me, except for 2 things:</p>  <ol>   <li>     <div align="left"><strong>Performance</strong>, if I installed a Windows operating system on a workstation en booted from it, it was much, much faster then when I used a Virtual Machine containing the same windows operation system on that same workstation.</div>   </li>    <li>     <div align="left"><strong>Snapshot – Backup host</strong>, if I installed a program or driver on the host and that corrupted the host, there was no out of the box recovery (yes there where al kinds of products that can do that, but not windows out of the box) possibility. <font color="#804040">One trick I used was to install an windows host OS and then only installed VMware Workstation on it. I would only use the VMware virtual machines and only used the host OS to take snapshots and backups of my virtual machines.</font></div>   </li> </ol>  <p align="left"><font color="#804040"></font></p>  <p align="left"><strong>VMware Workstation 7 (paid product)</strong></p>  <p align="left">Part 2 worked fine for me, but then I shifted from being a C# developer to a self-service BI specialist and Microsoft introduced PowerPivot and SharePoint 2010. In late 2009 I started to work with PowerPivot (Gemini at the time) and SharePoint 2010, so I create a VMware 7 development virtual machine with Microsoft Windows 2008 R2, Microsoft SQL Server 2008 R2, Microsoft SharePoint 2010 and Microsoft Office 2010 on a 3 year old dell laptop with 4 GB memory. Well that really did not perform at all. I bought a 80 GB Intel Postville G2 M-25 SSD, but the VMware Workstation virtual machine would not perform well and I was waiting on the system all of the time. Then one time I installed Microsoft Windows 2008 R2 as host OS with Microsoft SharePoint 2010 and PowerPivot on it. Well I was really impressed by the speed of the system, I booted in 3 times as fast an all Office products would directly open when I clicked on a document, instead of waiting for the splash screen. I know 4GB of RAM is not enough for a Microsoft SharePoint 2010 PowerPivot development machine, but with the help of the SSD I could manage it. But then I could not take snapshots of my host. </p>  <p align="left">As I said before, VMware Workstation 7 is to slow for me on my hardware for running Microsoft SharePoint 2010 with PowerPivot, that's why I started to look at hypervisors.</p>  <p align="left">Pros   <br />- Don’t have to no anything about hypervisors, just install windows host OS and then install VMware Workstation 7.0, it’s only a program.    <br />- Supports not only Windows guest operating systems    <br />    <br />Cons    <br />- Must be installed on a host operating system (host operating systems consumes cpu, memory and disk space    <br />- Is not free    <br />- “Bad” performance compared to native boot</p>  <p align="left">&#160;</p>  <p align="left"><strong>VMware ESXi (freeware)</strong></p>  <p align="left">Then in begin 2010 I learned about hypervisors. VMware has a free product ESXi 4, that can be installed on a system with a (32MB foot print, maximizing the space on the 80GB OS for Virtual Machines) and then you can run different virtual machine containing not only Microsoft OS but also Linux etc without installing a Host OS and having the possibility to take snapshots and backups of the virtual machines . So I created a bootable USB ESXi drive but found out my NIC and SATA controller where not supported, damn! Yes I know, ESXi is not supposed to be installed on a laptop but it would have been nice.</p>  <p align="left">Pros   <br />- Freeware    <br />- No host OS (so not need to snapshot or backup host, only snapshot and backup virtual machines)    <br />- 32 MB footprint    <br />- Supports not only Windows guest operating systems    <br />- Can run Microsoft Windows XP virtual machines     <br />- Can boot from USB without installing</p>  <p align="left">Cons   <br />- Can’t native boot from virtual machines (so a performance impact, but far better then VMware Workstation)    <br />- Could not get it to work with my DELL laptop</p>  <p align="left">&#160;</p>  <p align="left"><strong>Microsoft Hyper-V 2008 R2 (freeware)</strong></p>  <p align="left">In 2010 Microsoft released there hypervisor: Microsoft Hyper-V 2008 R2 and it’s free! What did you say, is Microsoft releasing a product that’s free of charge, the answer is; YES. It can be downloaded, here: <a title="http://www.microsoft.com/downloads/details.aspx?FamilyID=48359dd2-1c3d-4506-ae0a-232d0314ccf6&amp;displaylang=en" href="http://www.microsoft.com/downloads/details.aspx?FamilyID=48359dd2-1c3d-4506-ae0a-232d0314ccf6&amp;displaylang=en">http://www.microsoft.com/downloads/details.aspx?FamilyID=48359dd2-1c3d-4506-ae0a-232d0314ccf6&amp;displaylang=en</a> it’s a 1,5 GB ISO. Installed it and after installing I could boot from a VHD file created with Microsoft Windows 2008 R2</p>  <p align="left">Pros   <br />- Freeware    <br />- Native boot from VHD, maximizing performance and hardware possibilities    <br />- No host OS (so not need to snapshot or backup host, only snapshot and backup virtual machines)    <br />- 6GB footprint (after installing)    <br />- Can boot from USB without installing</p>  <p align="left">Cons   <br />- Supports only booting from Microsoft Windows 7 or Microsoft Windows Server 2008 R2    <br />- Have to use a “workstation” virtualization product in a booted virtual machine to manage other virtual machines</p>  <p align="left">&#160;</p>  <p align="left"><strong>What do I exactly use for developing Microsoft SharePoint 2010 PowerPivot applications</strong></p>  <p align="left">So today what do I exactly use for developing C# vs2008, C# vs2010 and SharePoint 2010 PowerPivot applications</p>  <ol>   <li>     <div align="left">Laptop with Microsoft Hyper-V Server 2008 R2 (freeware) installed on a 2,5 inch 80GB SSD boot disk, a 500GB 7200 rpm 2,5 inch for data and virtual machines I don’t often use and 8GB of RAM.</div>   </li>    <li>     <div align="left">When I start the laptop I boot into a VHD containing Microsoft Windows 2008 R2, Microsoft SQL Server 2008 R2, Microsoft SharePoint 2010, Microsoft Office 2010 and the hyper visor role installed to manage other virtual machines. Because I primarily do self service BI work and VS2010 development this is the machine I want the best performance for. I use the hyper-v manager in the this virtual machine to start legacy virtual machines (VS2005 with SQL 2005 or VS2008 with SQL 2008)</div>   </li>    <li>     <div align="left">In the SharePoint 2010 virtual machine I keep 2 images up date date, a base Microsoft Windows 7 and a base Microsoft Windows Server 2008 R2 virtual machine. They serve as base for creating new virtual machines, see <a title="http://www.roelvanlisdonk.nl/?p=1530" href="http://www.roelvanlisdonk.nl/?p=1530">http://www.roelvanlisdonk.nl/?p=1530</a>. They are updated every week and configured the way I want to, see <a title="http://www.roelvanlisdonk.nl/?p=1462" href="http://www.roelvanlisdonk.nl/?p=1462">http://www.roelvanlisdonk.nl/?p=1462</a></div>   </li>    <li>     <div align="left">In all I mange 6 virtual machines</div>   </li>    <ul>     <li>       <div align="left">Microsoft Windows 7 x64 - base for client virtual machines</div>     </li>      <li>       <div align="left">Microsoft Windows Server 2008 R2 x64 - base for server virtual machines</div>     </li>      <li>       <div align="left">Legacy 2005 development - clone of Microsoft Windows 7 x64 base containing VS2005, Office 2003, SQL Server 2005, SSIS 2005, SSRS 2005, SSAS 2005</div>     </li>      <li>       <div align="left">Legacy 2008 development - clone of Microsoft Windows 7 x64 base containing VS2008, Office 2007, SQL Server 2008, SSIS 2008, SSRS 2008, SSAS 2008</div>     </li>      <li>       <div align="left">SharePoint 2010 development (native boot), clone of Microsoft Windows Server 2008 R2 x64, containing VS2010, SharePoint 2010 with PowerPivot, Office 2010, SQL Server 2008 R2, SSIS 2008 R2, SSRS 2008 R2, SSAS 2008 R2</div>     </li>      <li>       <div align="left">VPN - clone of Microsoft Windows 7 x64 base containing VPN connections and remote desktop shortcuts to customer machines (I use a virtual machine for this purpose, because, when connected to the VPN I don’t have access to the rest of the network)</div>     </li>   </ul> </ol>  <p align="left">&#160;</p>  <p align="left"><strong>Conclusion</strong></p>  <p align="left">Microsoft Hyper-V Server 2008 R2 rules:</p>  <ol>   <li>     <div align="left"><font color="#0000ff">Creating new virtual machines in minutes, containing a fully patched windows host OS and configured the way I like it to be with the ability to boot from the virtual machines, maximizing performance</font></div>   </li>    <li>     <div align="left"><font color="#0000ff">Can use legacy development machines without rebooting (vs2005, vs2008 for legacy support)</font></div>   </li>    <li>     <div align="left"><font color="#0000ff">Install a full blown Microsoft SharePoint 2010 development server within 30 minutes on a new laptop or workstation and booting from it, maximizing performance</font></div>   </li> </ol>