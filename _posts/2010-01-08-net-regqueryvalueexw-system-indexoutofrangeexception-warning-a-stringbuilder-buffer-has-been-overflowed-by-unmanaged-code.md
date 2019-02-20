---
ID: 921
post_title: '.NET RegQueryValueExW System.IndexOutOfRangeException : Warning: A StringBuilder buffer has been overflowed by unmanaged code.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/01/08/net-regqueryvalueexw-system-indexoutofrangeexception-warning-a-stringbuilder-buffer-has-been-overflowed-by-unmanaged-code/
published: true
post_date: 2010-01-08 15:31:27
---
<p>If you get the error</p>  <p>System.IndexOutOfRangeException : Warning: A StringBuilder buffer has been overflowed by unmanaged code.&#160; The process may become unstable.&#160; Insufficient capacity allocated to the StringBuilder before marshaling it.   <br />&#160;&#160;&#160; at Ada.Cdf.Common.RegistryHelper.RegQueryValueExW(UIntPtr hKey, String lpValueName, Int32 lpReserved, UInt32&amp; lpType, StringBuilder lpData, UInt32&amp; lpcbData)</p>  <p>when reading a registry value, check the size of you´re string builder and the size of the RegQueryValueExW paramter lpcbData, these should be the same</p>  <pre class="code"><span style="color: blue">uint </span>size = <strong><font size="3">BufferMaxLength</font></strong>;
<span style="color: blue">uint </span>type;
<span style="color: blue">string </span>keyValue = <span style="color: blue">null</span>;
<span style="color: #2b91af">StringBuilder </span>keyBuffer = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<strong><font size="3">BufferMaxLength</font></strong>);
<span style="color: blue">string </span>keyname = <span style="color: #a31515">&quot;InstallLocation&quot;</span>;

<span style="color: green">// Get the data from the registrykeyvalue
</span><span style="color: blue">if </span>(RegQueryValueExW(regKeyHandle, keyname, 0, <span style="color: blue">out </span>type, keyBuffer, <span style="color: blue">ref </span><strong><font size="3">size</font></strong>) != Success)
{
    <span style="color: blue">throw new </span><span style="color: #2b91af">ApplicationException</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">@&quot;Could not find regstrykeyvalue [{0}\{1}]&quot;</span>, regKeyPath, keyname));
}</pre>
<a href="http://11011.net/software/vspaste"></a>