---
ID: 919
post_title: 'How to read the 32 bit part (Wow6432Node) of the registry from a x86 or x64 C# .net 3.5 application'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/01/08/how-to-read-the-32-bit-part-wow6432node-of-the-registry-from-a-x86-or-x64-c-net-3-5-application/
published: true
post_date: 2010-01-08 15:14:00
---
<p>Well in .NET 4.0 this will all change, but for know it you want to read a key from the registry and you don’t know if it’s in the 32 bits part of the registry or in the 64 bit part and you don’t know if you’re application will be compiled as x86 or x64 en you don’t know on which machine it will be deployed (x86 or x64). In fact you don´t know anything, you can use the GetRegistryKeyHandle function to try to find the key in the 64 bit part and then if not found try the find the key in the 32 bits part of the registry:</p>  <pre class="code"><span style="color: blue">public static </span><span style="color: #2b91af">UIntPtr </span>HKEY_CURRENT_USER = (<span style="color: #2b91af">UIntPtr</span>)0x80000001;
<span style="color: blue">public static </span><span style="color: #2b91af">UIntPtr </span>HKEY_LOCAL_MACHINE = (<span style="color: #2b91af">UIntPtr</span>)0x80000002;
<span style="color: blue">public static int </span>KEY_QUERY_VALUE = 0x0001;
<span style="color: blue">public static int </span>KEY_READ = 0x20019;

<span style="color: blue">public static int </span>KEY_SET_VALUE = 0x0002;
<span style="color: blue">public static int </span>KEY_CREATE_SUB_KEY = 0x0004;
<span style="color: blue">public static int </span>KEY_ENUMERATE_SUB_KEYS = 0x0008;
<span style="color: blue">public static int </span>KEY_WOW64_64KEY = 0x0100;
<span style="color: blue">public static int </span>KEY_WOW64_32KEY = 0x0200;

<span style="color: blue">public const int </span>Success = 0;
<span style="color: blue">public const int </span>FileNotFound = 2;
<span style="color: blue">public const int </span>AccessDenied = 5;
<span style="color: blue">public const int </span>InvalidParameter = 87;
<span style="color: blue">public const int </span>MoreData = 234;
<span style="color: blue">public const int </span>NoMoreEntries = 259;
<span style="color: blue">public const int </span>MarkedForDeletion = 1018;

<span style="color: blue">public const int </span>BufferMaxLength = 2048;

[<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;advapi32.dll&quot;</span>, CharSet = <span style="color: #2b91af">CharSet</span>.Unicode, EntryPoint = <span style="color: #a31515">&quot;RegOpenKeyExW&quot;</span>, SetLastError = <span style="color: blue">true</span>)]
<span style="color: blue">public static extern int </span>RegOpenKeyExW(<span style="color: #2b91af">UIntPtr </span>hKey, <span style="color: blue">string </span>subKey, <span style="color: blue">uint </span>options, <span style="color: blue">int </span>sam, <span style="color: blue">out </span><span style="color: #2b91af">UIntPtr </span>phkResult);

[<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;advapi32.dll&quot;</span>, CharSet = <span style="color: #2b91af">CharSet</span>.Unicode, EntryPoint = <span style="color: #a31515">&quot;RegEnumKeyW&quot;</span>)]
<span style="color: blue">private static extern int </span>RegEnumKeyW(<span style="color: #2b91af">UIntPtr </span>keyBase, <span style="color: blue">int </span>index, <span style="color: #2b91af">StringBuilder </span>nameBuffer, <span style="color: blue">int </span>bufferLength);</pre>

<pre class="code"><span style="color: gray">/// &lt;summary&gt;
///</span><span style="color: green">Try to find the regsitrykey in the 64 bit part of the registry.
</span><span style="color: gray">///</span><span style="color: green">If not found, try to find the registrykey in the 32 bit part of the registry.
</span><span style="color: gray">/// &lt;/summary&gt;
/// &lt;param name=&quot;regKeyPath&quot;&gt;&lt;/param&gt;
/// &lt;returns&gt;</span><span style="color: green">A registrykeyhandle</span><span style="color: gray">&lt;/returns&gt;
</span><span style="color: blue">public </span><span style="color: #2b91af">UIntPtr </span>GetRegistryKeyHandle(stringregKeyPath)
{
    <span style="color: #2b91af">UIntPtr </span>regKeyHandle;

    <span style="color: green">// Check parameters
   </span><span style="color: blue">if</span>(<span style="color: blue">string</span>.IsNullOrEmpty(regKeyPath)) { <span style="color: blue">throw </span>newArgumentNullException(<span style="color: #a31515">&quot;regKeyPath&quot;</span>, <span style="color: #a31515">&quot;GetRegistryKeyHandle: regKeyPath is null or empty.&quot;</span>); }

    <span style="color: green">// KEY_WOW64_64KEY
    // Access a 64-bit key from either a 32-bit or 64-bit application (not supported on Windows 2000).
    // 64-bit key = all keys in HKEY_LOCAL_MACHINE\Software except the HKEY_LOCAL_MACHINE\Software\Wow6432Node
    //
    // Check if the registrykey can be found in the 64 bit registry part of the register
   </span><span style="color: blue">if</span>(RegOpenKeyExW(HKEY_LOCAL_MACHINE, regKeyPath, 0, KEY_READ | KEY_WOW64_64KEY, outregKeyHandle) != Success)
    {
        <span style="color: green">// KEY_WOW64_32KEY
        // Access a 32-bit key from either a 32-bit or 64-bit application. (not supported on Windows 2000)
        // 32-bit key = all keys in HKEY_LOCAL_MACHINE\Software\Wow6432Node
        //
        // Check if the registrykey can be found in the 32 bit registry part of the register
       </span><span style="color: blue">if</span>(RegOpenKeyExW(HKEY_LOCAL_MACHINE, regKeyPath, 0, KEY_READ | KEY_WOW64_32KEY, outregKeyHandle) != Success)
        {
            <span style="color: blue">throw </span>newApplicationException(<span style="color: blue">string</span>.Format(<span style="color: #a31515">@&quot;GetRegistryKeyHandle: Could not find regstrykey [{0}\{1}]&quot;</span>, <span style="color: #2b91af">Registry</span>.LocalMachine, regKeyPath));
        }
    }

    <span style="color: blue">return </span>regKeyHandle;
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p><span style="color: blue">public void </span>LoopSubKeysTest()

  <br />{&#160; <span style="color: blue"></span></p>

<pre class="code"><span style="color: #2b91af">        UIntPtr </span>regKeyHandle = helper.GetRegistryKeyHandle(<span style="color: #a31515">@&quot;SOFTWARE\Microsoft\Windows\CurrentVersion\Installer\UpgradeCodes&quot;</span>);<br />
        <span style="color: #2b91af">StringBuilder </span>buffer = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(BufferMaxLength);
        <span style="color: blue">for </span>(<span style="color: blue">int </span>index = 0; <span style="color: blue">true</span>; index++)
        {
            <span style="color: blue">int </span>result = RegEnumKeyW(regKeyHandle, index, buffer, buffer.Capacity);

            <span style="color: blue">if </span>(result == Success)
            {
                <span style="color: #2b91af">Console</span>.WriteLine(buffer.ToString());
                buffer.Length = 0;
                <span style="color: blue">continue</span>;
            }

            <span style="color: blue">if </span>(result == NoMoreEntries) { <span style="color: blue">break</span>; };

            <span style="color: blue">throw new </span><span style="color: #2b91af">ApplicationException</span>(<span style="color: #a31515">&quot;This RegEnumKeyW result is unknown&quot;</span>);
        }
}</pre>
<a href="http://11011.net/software/vspaste"></a>