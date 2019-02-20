---
ID: 2521
post_title: >
  How to run Hyper-V on Windows 8 inside
  VMware Workstation 8
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/03/02/how-to-run-hyper-v-on-windows-8-inside-vmware-workstation-8/
published: true
post_date: 2012-03-02 15:09:01
---
&nbsp;

Before you read any further, as Dane pointed out, you can install Hyper-V on Microsoft Windows 8 Consumer Preview, but after rebooting you will be presented by a "blue screen", because a HAL_Memory_Allocation was thrown. This is broken since the beta build. Let’s hope they fix this in the RTM.

&nbsp;

Meet the power of |"Intel VT-x/EPT". Normally when you want to install Hyper-V on Windows 8 inside VMware Workstation 8 you will get the following message:

&nbsp;

<strong>Hyper-V cannot be installed: A hypervisor is already running.</strong>

&nbsp;

<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image.png" rel="lightbox"><img style="background-image: none; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb.png" alt="image" width="420" height="325" border="0" /></a>

&nbsp;

Shutdown the machine and edit the Virtual Machine Settings &gt; Hardware &gt; Processors &gt; check the "Virtualize Intel VT-x/EPT":

&nbsp;

<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image1.png" rel="lightbox"><img style="background-image: none; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb1.png" alt="image" width="577" height="500" border="0" /></a>

&nbsp;

One more thing you should do, is edit the vmx file of the Windows 8 VMware virtual machine and add the setting  "<strong>hypervisor.cpuid.v0 = "FALSE"</strong>, as described here: <a href="http://www.veeam.com/blog/nesting-hyper-v-with-vmware-workstation-8-and-esxi-5.html">http://www.veeam.com/blog/nesting-hyper-v-with-vmware-workstation-8-and-esxi-5.html</a>

&nbsp;

Now you can boot the Windows 8 VMware virtual machine and add install Hyper-V.

Go to Control Panel &gt; Programs and Features &gt; Turn Windows features on or off &gt;

<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image2.png" rel="lightbox"><img style="background-image: none; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb2.png" alt="image" width="550" height="166" border="0" /></a>

Now you will get the message: "Provides the services that you can use to create and manage virtual machines and their resources".

<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image3.png" rel="lightbox"><img style="background-image: none; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb3.png" alt="image" width="580" height="393" border="0" /></a>

&nbsp;

&nbsp;

&nbsp;

More information can be found, here: <a href="http://virtualizedgeek.com/2011/09/16/nested-win8-hyperv/">http://virtualizedgeek.com/2011/09/16/nested-win8-hyperv/</a>