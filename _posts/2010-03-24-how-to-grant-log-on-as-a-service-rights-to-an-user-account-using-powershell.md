---
ID: 1151
post_title: 'How to grant &ldquo;Log on as a service&rdquo; rights to an user account, using PowerShell'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/24/how-to-grant-log-on-as-a-service-rights-to-an-user-account-using-powershell/
published: true
post_date: 2010-03-24 13:54:08
---
<p>If you want to grant “Log on as a service” rights to a user account, using PowerShell you can use the secedit.exe tool, using a *.inf security template file. </p>  <p>&#160;</p>  <p><strong>[Script]</strong></p>  <p>secedit /import /db secedit.sdb /cfg &quot;C:\Temp\MySecurityTemplate.inf&quot; /silent &gt;nul</p>  <p>gpupdate /force</p>  <p>&#160;</p>  <p><strong>[MySecurityTemplate.inf]</strong></p>  <p>[Unicode]   <br />Unicode=yes    <br />[Version]    <br />signature=&quot;$CHICAGO$&quot;    <br />Revision=1    <br />[Registry Values]    <br />[Profile Description]    <br />Description=Set log on as a service etc    <br />[Privilege Rights]    <br />SeServiceLogonRight = *S-1-5-21-3051157669-1303869509-1073059025-1019</p>  <p>&#160;</p>  <p>You can generate the “C:\Temp\MySecurityTemplate.inf” by following the steps on <a title="http://msdn.microsoft.com/en-us/library/ms933182(WinEmbedded.5).aspx" href="http://msdn.microsoft.com/en-us/library/ms933182(WinEmbedded.5).aspx">http://msdn.microsoft.com/en-us/library/ms933182(WinEmbedded.5).aspx</a></p>  <p>&#160;</p>  <p><strong>[But in some cases, this was not what I wanted]</strong></p>  <p>An other solution, is to P/Invoke the LSA functions in the advapi32.dl with C#.</p>  <p>Willy created a LSA wrapper for C#: <a title="http://www.developmentnow.com/g/36_2005_3_0_0_223925/LSA-functions.htm" href="http://www.developmentnow.com/g/36_2005_3_0_0_223925/LSA-functions.htm">http://www.developmentnow.com/g/36_2005_3_0_0_223925/LSA-functions.htm</a></p>  <p>I used this wrapper class to grant “Log on as a service” rights to an user account, using PowerShell</p>  <p>After building the assembly containing the LSA wrapper class, you can grant access with this PowerShell script:</p>  <p>&#160;</p>  <p><strong>[Test.ps1]</strong></p>  <p># [General]   <br />&quot;Set execution policy to [Unrestricted]&quot;     <br />Set-ExecutionPolicy Unrestricted </p>  <p>&quot;Load assemblies&quot;   <br />$assemblyLsa = &quot;C:\Temp\MyLsaWrapper.dll&quot;    <br />[System.Reflection.Assembly]::LoadFrom($assemblyLsa)    <br /></p>  <p>“Grant Log on as a service rights to the account MyComputer\User1”</p>  <p>[MyLsaWrapper.LsaWrapperCaller]::(&quot;MyComputer\User1&quot;, &quot;SeServiceLogonRight&quot;)</p>  <p>&#160;</p>  <p>&#160;</p>  <p><strong>[LsaWrapper in C#]</strong></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;


<span style="color: blue">namespace </span>MyLsaWrapper
{
    <span style="color: blue">using </span>System.Runtime.InteropServices;
    <span style="color: blue">using </span>System.Security;
    <span style="color: blue">using </span>System.Management;
    <span style="color: blue">using </span>System.Runtime.CompilerServices;
    <span style="color: blue">using </span>System.ComponentModel;

    <span style="color: blue">using </span><span style="color: #2b91af">LSA_HANDLE </span>= <span style="color: #2b91af">IntPtr</span>;

    [<span style="color: #2b91af">StructLayout</span>(<span style="color: #2b91af">LayoutKind</span>.Sequential)]
    <span style="color: blue">struct </span><span style="color: #2b91af">LSA_OBJECT_ATTRIBUTES
    </span>{
        <span style="color: blue">internal int </span>Length;
        <span style="color: blue">internal </span><span style="color: #2b91af">IntPtr </span>RootDirectory;
        <span style="color: blue">internal </span><span style="color: #2b91af">IntPtr </span>ObjectName;
        <span style="color: blue">internal int </span>Attributes;
        <span style="color: blue">internal </span><span style="color: #2b91af">IntPtr </span>SecurityDescriptor;
        <span style="color: blue">internal </span><span style="color: #2b91af">IntPtr </span>SecurityQualityOfService;
    }
    [<span style="color: #2b91af">StructLayout</span>(<span style="color: #2b91af">LayoutKind</span>.Sequential, CharSet = <span style="color: #2b91af">CharSet</span>.Unicode)]
    <span style="color: blue">struct </span><span style="color: #2b91af">LSA_UNICODE_STRING
    </span>{
        <span style="color: blue">internal ushort </span>Length;
        <span style="color: blue">internal ushort </span>MaximumLength;
        [<span style="color: #2b91af">MarshalAs</span>(<span style="color: #2b91af">UnmanagedType</span>.LPWStr)]
        <span style="color: blue">internal string </span>Buffer;
    }
    <span style="color: blue">sealed class </span><span style="color: #2b91af">Win32Sec
    </span>{
        [<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;advapi32&quot;</span>, CharSet = <span style="color: #2b91af">CharSet</span>.Unicode, SetLastError = <span style="color: blue">true</span>),
        <span style="color: #2b91af">SuppressUnmanagedCodeSecurityAttribute</span>]
        <span style="color: blue">internal static extern uint </span>LsaOpenPolicy(
        <span style="color: #2b91af">LSA_UNICODE_STRING</span>[] SystemName,
        <span style="color: blue">ref </span><span style="color: #2b91af">LSA_OBJECT_ATTRIBUTES </span>ObjectAttributes,
        <span style="color: blue">int </span>AccessMask,
        <span style="color: blue">out </span><span style="color: #2b91af">IntPtr </span>PolicyHandle
        );

        [<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;advapi32&quot;</span>, CharSet = <span style="color: #2b91af">CharSet</span>.Unicode, SetLastError = <span style="color: blue">true</span>),
        <span style="color: #2b91af">SuppressUnmanagedCodeSecurityAttribute</span>]
        <span style="color: blue">internal static extern uint </span>LsaAddAccountRights(
        <span style="color: #2b91af">LSA_HANDLE </span>PolicyHandle,
        <span style="color: #2b91af">IntPtr </span>pSID,
        <span style="color: #2b91af">LSA_UNICODE_STRING</span>[] UserRights,
        <span style="color: blue">int </span>CountOfRights
        );

        [<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;advapi32&quot;</span>, CharSet = <span style="color: #2b91af">CharSet</span>.Unicode, SetLastError = <span style="color: blue">true</span>),
        <span style="color: #2b91af">SuppressUnmanagedCodeSecurityAttribute</span>]
        <span style="color: blue">internal static extern int </span>LsaLookupNames2(
        <span style="color: #2b91af">LSA_HANDLE </span>PolicyHandle,
        <span style="color: blue">uint </span>Flags,
        <span style="color: blue">uint </span>Count,
        <span style="color: #2b91af">LSA_UNICODE_STRING</span>[] Names,
        <span style="color: blue">ref </span><span style="color: #2b91af">IntPtr </span>ReferencedDomains,
        <span style="color: blue">ref </span><span style="color: #2b91af">IntPtr </span>Sids
        );

        [<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;advapi32&quot;</span>)]
        <span style="color: blue">internal static extern int </span>LsaNtStatusToWinError(<span style="color: blue">int </span>NTSTATUS);

        [<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;advapi32&quot;</span>)]
        <span style="color: blue">internal static extern int </span>LsaClose(<span style="color: #2b91af">IntPtr </span>PolicyHandle);

        [<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;advapi32&quot;</span>)]
        <span style="color: blue">internal static extern int </span>LsaFreeMemory(<span style="color: #2b91af">IntPtr </span>Buffer);

    }
    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">This class is used to grant &quot;Log on as a service&quot;, &quot;Log on as a batchjob&quot;, &quot;Log on localy&quot; etc.
    </span><span style="color: gray">/// </span><span style="color: green">to a user.
    </span><span style="color: gray">/// &lt;/summary&gt;
    </span><span style="color: blue">public sealed class </span><span style="color: #2b91af">LsaWrapper </span>: <span style="color: #2b91af">IDisposable
    </span>{
        [<span style="color: #2b91af">StructLayout</span>(<span style="color: #2b91af">LayoutKind</span>.Sequential)]
        <span style="color: blue">struct </span><span style="color: #2b91af">LSA_TRUST_INFORMATION
        </span>{
            <span style="color: blue">internal </span><span style="color: #2b91af">LSA_UNICODE_STRING </span>Name;
            <span style="color: blue">internal </span><span style="color: #2b91af">IntPtr </span>Sid;
        }
        [<span style="color: #2b91af">StructLayout</span>(<span style="color: #2b91af">LayoutKind</span>.Sequential)]
        <span style="color: blue">struct </span><span style="color: #2b91af">LSA_TRANSLATED_SID2
        </span>{
            <span style="color: blue">internal </span><span style="color: #2b91af">SidNameUse </span>Use;
            <span style="color: blue">internal </span><span style="color: #2b91af">IntPtr </span>Sid;
            <span style="color: blue">internal int </span>DomainIndex;
            <span style="color: blue">uint </span>Flags;
        }

        [<span style="color: #2b91af">StructLayout</span>(<span style="color: #2b91af">LayoutKind</span>.Sequential)]
        <span style="color: blue">struct </span><span style="color: #2b91af">LSA_REFERENCED_DOMAIN_LIST
        </span>{
            <span style="color: blue">internal uint </span>Entries;
            <span style="color: blue">internal </span><span style="color: #2b91af">LSA_TRUST_INFORMATION </span>Domains;
        }

        <span style="color: blue">enum </span><span style="color: #2b91af">SidNameUse </span>: <span style="color: blue">int
        </span>{
            User = 1,
            Group = 2,
            Domain = 3,
            Alias = 4,
            KnownGroup = 5,
            DeletedAccount = 6,
            Invalid = 7,
            Unknown = 8,
            Computer = 9
        }

        <span style="color: blue">enum </span><span style="color: #2b91af">Access </span>: <span style="color: blue">int
        </span>{
            POLICY_READ = 0x20006,
            POLICY_ALL_ACCESS = 0x00F0FFF,
            POLICY_EXECUTE = 0X20801,
            POLICY_WRITE = 0X207F8
        }
        <span style="color: blue">const uint </span>STATUS_ACCESS_DENIED = 0xc0000022;
        <span style="color: blue">const uint </span>STATUS_INSUFFICIENT_RESOURCES = 0xc000009a;
        <span style="color: blue">const uint </span>STATUS_NO_MEMORY = 0xc0000017;

        <span style="color: #2b91af">IntPtr </span>lsaHandle;

        <span style="color: blue">public </span>LsaWrapper()
            : <span style="color: blue">this</span>(<span style="color: blue">null</span>)
        { }
        <span style="color: green">// // local system if systemName is null
        </span><span style="color: blue">public </span>LsaWrapper(<span style="color: blue">string </span>systemName)
        {
            <span style="color: #2b91af">LSA_OBJECT_ATTRIBUTES </span>lsaAttr;
            lsaAttr.RootDirectory = <span style="color: #2b91af">IntPtr</span>.Zero;
            lsaAttr.ObjectName = <span style="color: #2b91af">IntPtr</span>.Zero;
            lsaAttr.Attributes = 0;
            lsaAttr.SecurityDescriptor = <span style="color: #2b91af">IntPtr</span>.Zero;
            lsaAttr.SecurityQualityOfService = <span style="color: #2b91af">IntPtr</span>.Zero;
            lsaAttr.Length = <span style="color: #2b91af">Marshal</span>.SizeOf(<span style="color: blue">typeof</span>(<span style="color: #2b91af">LSA_OBJECT_ATTRIBUTES</span>));
            lsaHandle = <span style="color: #2b91af">IntPtr</span>.Zero;
            <span style="color: #2b91af">LSA_UNICODE_STRING</span>[] system = <span style="color: blue">null</span>;
            <span style="color: blue">if </span>(systemName != <span style="color: blue">null</span>)
            {
                system = <span style="color: blue">new </span><span style="color: #2b91af">LSA_UNICODE_STRING</span>[1];
                system[0] = InitLsaString(systemName);
            }

            <span style="color: blue">uint </span>ret = <span style="color: #2b91af">Win32Sec</span>.LsaOpenPolicy(system, <span style="color: blue">ref </span>lsaAttr,
            (<span style="color: blue">int</span>)<span style="color: #2b91af">Access</span>.POLICY_ALL_ACCESS, <span style="color: blue">out </span>lsaHandle);
            <span style="color: blue">if </span>(ret == 0)
                <span style="color: blue">return</span>;
            <span style="color: blue">if </span>(ret == STATUS_ACCESS_DENIED)
            {
                <span style="color: blue">throw new </span><span style="color: #2b91af">UnauthorizedAccessException</span>();
            }
            <span style="color: blue">if </span>((ret == STATUS_INSUFFICIENT_RESOURCES) || (ret == STATUS_NO_MEMORY))
            {
                <span style="color: blue">throw new </span><span style="color: #2b91af">OutOfMemoryException</span>();
            }
            <span style="color: blue">throw new </span><span style="color: #2b91af">Win32Exception</span>(<span style="color: #2b91af">Win32Sec</span>.LsaNtStatusToWinError((<span style="color: blue">int</span>)ret));
        }

        <span style="color: blue">public void </span>AddPrivileges(<span style="color: blue">string </span>account, <span style="color: blue">string </span>privilege)
        {
            <span style="color: #2b91af">IntPtr </span>pSid = GetSIDInformation(account);
            <span style="color: #2b91af">LSA_UNICODE_STRING</span>[] privileges = <span style="color: blue">new </span><span style="color: #2b91af">LSA_UNICODE_STRING</span>[1];
            privileges[0] = InitLsaString(privilege);
            <span style="color: blue">uint </span>ret = <span style="color: #2b91af">Win32Sec</span>.LsaAddAccountRights(lsaHandle, pSid, privileges, 1);
            <span style="color: blue">if </span>(ret == 0)
                <span style="color: blue">return</span>;
            <span style="color: blue">if </span>(ret == STATUS_ACCESS_DENIED)
            {
                <span style="color: blue">throw new </span><span style="color: #2b91af">UnauthorizedAccessException</span>();
            }
            <span style="color: blue">if </span>((ret == STATUS_INSUFFICIENT_RESOURCES) || (ret == STATUS_NO_MEMORY))
            {
                <span style="color: blue">throw new </span><span style="color: #2b91af">OutOfMemoryException</span>();
            }
            <span style="color: blue">throw new </span><span style="color: #2b91af">Win32Exception</span>(<span style="color: #2b91af">Win32Sec</span>.LsaNtStatusToWinError((<span style="color: blue">int</span>)ret));
        }


        <span style="color: blue">public void </span>Dispose()
        {
            <span style="color: blue">if </span>(lsaHandle != <span style="color: #2b91af">IntPtr</span>.Zero)
            {
                <span style="color: #2b91af">Win32Sec</span>.LsaClose(lsaHandle);
                lsaHandle = <span style="color: #2b91af">IntPtr</span>.Zero;
            }
            <span style="color: #2b91af">GC</span>.SuppressFinalize(<span style="color: blue">this</span>);
        }
        ~LsaWrapper()
        {
            Dispose();
        }
        <span style="color: green">// helper functions

        </span><span style="color: #2b91af">IntPtr </span>GetSIDInformation(<span style="color: blue">string </span>account)
        {
            <span style="color: #2b91af">LSA_UNICODE_STRING</span>[] names = <span style="color: blue">new </span><span style="color: #2b91af">LSA_UNICODE_STRING</span>[1];
            <span style="color: #2b91af">LSA_TRANSLATED_SID2 </span>lts;
            <span style="color: #2b91af">IntPtr </span>tsids = <span style="color: #2b91af">IntPtr</span>.Zero;
            <span style="color: #2b91af">IntPtr </span>tdom = <span style="color: #2b91af">IntPtr</span>.Zero;
            names[0] = InitLsaString(account);
            lts.Sid = <span style="color: #2b91af">IntPtr</span>.Zero;
            <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: #a31515">&quot;String account: {0}&quot;</span>, names[0].Length);
            <span style="color: blue">int </span>ret = <span style="color: #2b91af">Win32Sec</span>.LsaLookupNames2(lsaHandle, 0, 1, names, <span style="color: blue">ref </span>tdom, <span style="color: blue">ref </span>tsids);
            <span style="color: blue">if </span>(ret != 0)
                <span style="color: blue">throw new </span><span style="color: #2b91af">Win32Exception</span>(<span style="color: #2b91af">Win32Sec</span>.LsaNtStatusToWinError(ret));
            lts = (<span style="color: #2b91af">LSA_TRANSLATED_SID2</span>)<span style="color: #2b91af">Marshal</span>.PtrToStructure(tsids,
            <span style="color: blue">typeof</span>(<span style="color: #2b91af">LSA_TRANSLATED_SID2</span>));
            <span style="color: #2b91af">Win32Sec</span>.LsaFreeMemory(tsids);
            <span style="color: #2b91af">Win32Sec</span>.LsaFreeMemory(tdom);
            <span style="color: blue">return </span>lts.Sid;
        }

        <span style="color: blue">static </span><span style="color: #2b91af">LSA_UNICODE_STRING </span>InitLsaString(<span style="color: blue">string </span>s)
        {
            <span style="color: green">// Unicode strings max. 32KB
            </span><span style="color: blue">if </span>(s.Length &gt; 0x7ffe)
                <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentException</span>(<span style="color: #a31515">&quot;String too long&quot;</span>);
            <span style="color: #2b91af">LSA_UNICODE_STRING </span>lus = <span style="color: blue">new </span><span style="color: #2b91af">LSA_UNICODE_STRING</span>();
            lus.Buffer = s;
            lus.Length = (<span style="color: blue">ushort</span>)(s.Length * <span style="color: blue">sizeof</span>(<span style="color: blue">char</span>));
            lus.MaximumLength = (<span style="color: blue">ushort</span>)(lus.Length + <span style="color: blue">sizeof</span>(<span style="color: blue">char</span>));
            <span style="color: blue">return </span>lus;
        }
    }
    <span style="color: blue">public class </span><span style="color: #2b91af">LsaWrapperCaller
    </span>{
        <span style="color: blue">public static void </span>AddPrivileges(<span style="color: blue">string </span>account, <span style="color: blue">string </span>privilege)
        {
            <span style="color: blue">using </span>(<span style="color: #2b91af">LsaWrapper </span>lsaWrapper = <span style="color: blue">new </span><span style="color: #2b91af">LsaWrapper</span>())
            {
                lsaWrapper.AddPrivileges(account, privilege);
            }
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>