---
ID: 708
post_title: >
  How to convert a unicode string to an
  ASCII string
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/09/15/how-to-convert-a-unicode-string-to-an-ascii-string/
published: true
post_date: 2009-09-15 14:36:42
---
<p>To convert a unicode string to an ASCII string, use:   <br /></p>  <pre class="code"><span style="color: blue">        public void </span>ConvertUnicodeStringToAsciiString()
        {
            <span style="color: green">// Create two different encodings.
            </span><span style="color: #2b91af">Encoding </span>ascii = <span style="color: #2b91af">Encoding</span>.ASCII;
            <span style="color: #2b91af">Encoding </span>unicode = <span style="color: #2b91af">Encoding</span>.Unicode;

            <span style="color: green">// Convert the string into a byte[].
            </span><span style="color: blue">byte</span>[] unicodeBytes = unicode.GetBytes(<span style="color: #a31515">&quot;van ’t huis&quot;</span>);

            <span style="color: green">// Perform the conversion from one encoding to the other.
            </span><span style="color: blue">byte</span>[] asciiBytes = <span style="color: #2b91af">Encoding</span>.Convert(unicode, ascii, unicodeBytes);
            <span style="color: blue">char</span>[] asciiChars = <span style="color: blue">new char</span>[ascii.GetCharCount(asciiBytes, 0, asciiBytes.Length)];
            ascii.GetChars(asciiBytes, 0, asciiBytes.Length, asciiChars, 0);
            <span style="color: blue">string </span>asciiString = <span style="color: blue">new string</span>(asciiChars);
            <span style="color: #2b91af">Console</span>.WriteLine(asciiString);
        }</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>See: <a title="http://msdn.microsoft.com/en-us/library/system.text.encoding.convert(VS.71).aspx" href="http://msdn.microsoft.com/en-us/library/system.text.encoding.convert(VS.71).aspx">http://msdn.microsoft.com/en-us/library/system.text.encoding.convert(VS.71).aspx</a></p>