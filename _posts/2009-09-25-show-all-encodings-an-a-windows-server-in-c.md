---
ID: 718
post_title: 'Show all encodings and codepages on a Windows server in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/09/25/show-all-encodings-an-a-windows-server-in-c/
published: true
post_date: 2009-09-25 09:23:28
---
<p>If you want to show all encodings of a Windows server in C# in sorted order, use the code:</p><pre class="code"><span style="color: green">    // Get all encodings know on this server
    </span><span style="color: #2b91af">EncodingInfo</span>[] encodings = <span style="color: #2b91af">Encoding</span>.GetEncodings();

    <span style="color: green">// Sort EncodingInfo array by Name
    </span><span style="color: #2b91af">Array</span>.Sort(encodings, <span style="color: blue">new </span><span style="color: #2b91af">CaseInsensitiveEncodingInfoNameComparer</span>());

    <span style="color: green">// Show all encodings
    </span><span style="color: blue">foreach </span>(<span style="color: #2b91af">EncodingInfo </span>encoding <span style="color: blue">in </span>encodings)
    {
        <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">"{0}"</span>, encoding.Name));
    }</pre><pre class="code"><span style="color: blue">    public class </span><span style="color: #2b91af">CaseInsensitiveEncodingInfoNameComparer </span>: <span style="color: #2b91af">IComparer
    </span>{
        <span style="color: green">// Compare 2 EncodingInfo objects, by doing a case insensitive compare on there name
        </span><span style="color: blue">int </span><span style="color: #2b91af">IComparer</span>.Compare(<span style="color: #2b91af">Object </span>x, <span style="color: #2b91af">Object </span>y)
        {
            <span style="color: blue">int </span>result = 0;
            <span style="color: blue">if </span>(x <span style="color: blue">is </span><span style="color: #2b91af">EncodingInfo </span>&amp;&amp; y <span style="color: blue">is </span><span style="color: #2b91af">EncodingInfo</span>)
            {
                <span style="color: blue">var </span>xEncodingInfo = x <span style="color: blue">as </span><span style="color: #2b91af">EncodingInfo</span>;
                <span style="color: blue">var </span>yEncodingInfo = y <span style="color: blue">as </span><span style="color: #2b91af">EncodingInfo</span>;
                result = ((<span style="color: blue">new </span><span style="color: #2b91af">CaseInsensitiveComparer</span>()).Compare(xEncodingInfo.Name, yEncodingInfo.Name));
            }
            <span style="color: blue">return </span>result;
        }
    }</pre><a href="http://11011.net/software/vspaste"></a><pre class="code">&nbsp;</pre><pre class="code">&nbsp;</pre><a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>
<p>Result:<br /></p>
<p>ASMO-708<br />big5<br />cp1025<br />cp866<br />cp875<br />csISO2022JP<br />DOS-720<br />DOS-862<br />EUC-CN<br />EUC-JP<br />euc-jp<br />euc-kr<br />GB18030<br />gb2312<br />hz-gb-2312<br />IBM00858<br />IBM00924<br />IBM01047<br />IBM01140<br />IBM01141<br />IBM01142<br />IBM01143<br />IBM01144<br />IBM01145<br />IBM01146<br />IBM01147<br />IBM01148<br />IBM01149<br />IBM037<br />IBM1026<br />IBM273<br />IBM277<br />IBM278<br />IBM280<br />IBM284<br />IBM285<br />IBM290<br />IBM297<br />IBM420<br />IBM423<br />IBM424<br />IBM437<br />IBM500<br />ibm737<br />ibm775<br />ibm850<br />ibm852<br />IBM855<br />ibm857<br />IBM860<br />ibm861<br />IBM863<br />IBM864<br />IBM865<br />ibm869<br />IBM870<br />IBM871<br />IBM880<br />IBM905<br />IBM-Thai<br />iso-2022-jp<br />iso-2022-jp<br />iso-2022-kr<br />iso-8859-1<br />iso-8859-13<br />iso-8859-15<br />iso-8859-2<br />iso-8859-3<br />iso-8859-4<br />iso-8859-5<br />iso-8859-6<br />iso-8859-7<br />iso-8859-8<br />iso-8859-8-i<br />iso-8859-9<br />Johab<br />koi8-r<br />koi8-u<br />ks_c_5601-1987<br />macintosh<br />shift_jis<br />unicodeFFFE<br />us-ascii<br />utf-16<br />utf-32<br />utf-32BE<br />utf-7<br />utf-8<br />windows-1250<br />windows-1251<br />Windows-1252<br />windows-1253<br />windows-1254<br />windows-1255<br />windows-1256<br />windows-1257<br />windows-1258<br />windows-874<br />x-Chinese-CNS<br />x-Chinese-Eten<br />x-cp20001<br />x-cp20003<br />x-cp20004<br />x-cp20005<br />x-cp20261<br />x-cp20269<br />x-cp20936<br />x-cp20949<br />x-cp50227<br />x-EBCDIC-KoreanExtended<br />x-Europa<br />x-IA5<br />x-IA5-German<br />x-IA5-Norwegian<br />x-IA5-Swedish<br />x-iscii-as<br />x-iscii-be<br />x-iscii-de<br />x-iscii-gu<br />x-iscii-ka<br />x-iscii-ma<br />x-iscii-or<br />x-iscii-pa<br />x-iscii-ta<br />x-iscii-te<br />x-mac-arabic<br />x-mac-ce<br />x-mac-chinesesimp<br />x-mac-chinesetrad<br />x-mac-croatian<br />x-mac-cyrillic<br />x-mac-greek<br />x-mac-hebrew<br />x-mac-icelandic<br />x-mac-japanese<br />x-mac-korean<br />x-mac-romanian<br />x-mac-thai<br />x-mac-turkish<br />x-mac-ukrainian</p><a href="http://11011.net/software/vspaste"></a>