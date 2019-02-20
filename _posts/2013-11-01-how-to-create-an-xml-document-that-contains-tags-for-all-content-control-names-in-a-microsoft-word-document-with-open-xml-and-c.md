---
ID: 3523
post_title: 'How to create an XML document that contains tags for all content control names in a Microsoft Word document, with Open XML and C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/11/01/how-to-create-an-xml-document-that-contains-tags-for-all-content-control-names-in-a-microsoft-word-document-with-open-xml-and-c/
published: true
post_date: 2013-11-01 10:51:34
---
<p>&#160;</p>  <p>If you want to bind content controls in a Microsoft Word document to data, you might want to use a CustomXmlPart. This is a XML document that binds content controls to xml tag names.</p>  <p>&#160;</p>  <p>The xml produced will look like:</p>  <pre class="code"><span style="background: white; color: blue">&lt;?</span><span style="background: white; color: #a31515">xml </span><span style="background: white; color: red">version</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">1.0</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">encoding</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">utf-8</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">?&gt;
&lt;</span><span style="background: white; color: #a31515">Root</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Employee_EmployeeCity</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Employee_EmployeeCity</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Employee_CompetitionAttachment</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Employee_CompetitionAttachment</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Employee_FirstName</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Employee_FirstName</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Employee_FormattedName</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Employee_FormattedName</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Employee_HandinDate</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Employee_HandinDate</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Employee_HouseNumber</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Employee_HouseNumber</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Employee_HouseSuffix</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Employee_HouseSuffix</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Employee_PostalCode</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Employee_PostalCode</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Employee_RelationAttachment</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Employee_RelationAttachment</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Employee_Salutation</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Employee_Salutation</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Employee_Street</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Employee_Street</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Enlistment_CompetitionClause</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Enlistment_CompetitionClause</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Enlistment_EmployeeFirstDay</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Enlistment_EmployeeFirstDay</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Enlistment_RelationshipClause</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Enlistment_RelationshipClause</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Enlistment_TraineeTravel</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Enlistment_TraineeTravel</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Function_CurrentDate</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Function_CurrentDate</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">Function_GetManager</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">Function_GetManager</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">ServiceRequest_Id</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: #a31515">ServiceRequest_Id</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: #a31515">Root</span><span style="background: white; color: blue">&gt;</span></pre>


<p>&#160;</p>

<p>To produce that XML document based on all content control names in a Microsoft Word document, you can use the following code:</p>

<pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">EndToEndTest
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">DocumentFormat.OpenXml;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">DocumentFormat.OpenXml.Packaging;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">DocumentFormat.OpenXml.Wordprocessing;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.IO;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Xml.Linq;
    

    [</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">RliResearch
    </span><span style="background: white; color: black">{
        [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Test_with_duration()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">watch = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">System.Diagnostics.</span><span style="background: white; color: #2b91af">Stopwatch</span><span style="background: white; color: black">();
            watch.Start();

            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">sourcePath = </span><span style="background: white; color: #a31515">@&quot;C:\Temp\Test.docx&quot;</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">destinationPath = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">@&quot;C:\Temp\{0}_Test.xml&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #2b91af">Guid</span><span style="background: white; color: black">.NewGuid());
            Create_XML_file_for_CustomXmlPart(sourcePath, destinationPath);

            watch.Stop();
            System.</span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(watch.Elapsed.TotalMilliseconds);
        }

        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Create_XML_file_for_CustomXmlPart(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">sourcePath, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">destinationPath)
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">names = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt;();
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">Stream </span><span style="background: white; color: black">content = GetFileContent(sourcePath))
            {
                names = GetUniqueContentControlNames(content);
            }

            </span><span style="background: white; color: #2b91af">XDocument </span><span style="background: white; color: black">document = CreateXmlDocument(</span><span style="background: white; color: #a31515">&quot;Root&quot;</span><span style="background: white; color: black">, names);

            document.Save(destinationPath);
        }

        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Gets the contents of the file as a stream, don't forget to use this function in a &quot;using&quot; statement.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">Stream </span><span style="background: white; color: black">GetFileContent(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">path)
        {
            </span><span style="background: white; color: blue">byte</span><span style="background: white; color: black">[] contentBytes = </span><span style="background: white; color: #2b91af">File</span><span style="background: white; color: black">.ReadAllBytes(path);
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">stream = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">MemoryStream</span><span style="background: white; color: black">(contentBytes);
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">stream;
        }

        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Create a XDocument, with a root element based on the given &quot;rootName&quot;, containing child elements based on the given &quot;tagnames&quot;.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">XDocument </span><span style="background: white; color: black">CreateXmlDocument(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">rootName, </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt; tagNames)
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">document = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">XDocument</span><span style="background: white; color: black">(
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">XDeclaration</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;1.0&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;utf-8&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">),
                    </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">XElement</span><span style="background: white; color: black">(rootName,
                        tagNames.Select(x =&gt; </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">XElement</span><span style="background: white; color: black">(x, </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Empty)
                    )
                )
            );

            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">document;
        }

        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Gets all unique content control names in the given document.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt; GetUniqueContentControlNames(</span><span style="background: white; color: #2b91af">Stream </span><span style="background: white; color: black">content)
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">names = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt;();
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">WordprocessingDocument </span><span style="background: white; color: black">doc =
            </span><span style="background: white; color: #2b91af">WordprocessingDocument</span><span style="background: white; color: black">.Open(content, </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">))
            {
                </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">cc </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">doc.ContentControls())
                {
                    </span><span style="background: white; color: #2b91af">SdtProperties </span><span style="background: white; color: black">props = cc.Elements&lt;</span><span style="background: white; color: #2b91af">SdtProperties</span><span style="background: white; color: black">&gt;().FirstOrDefault();
                    </span><span style="background: white; color: #2b91af">Tag </span><span style="background: white; color: black">tag = props.Elements&lt;</span><span style="background: white; color: #2b91af">Tag</span><span style="background: white; color: black">&gt;().FirstOrDefault();
                    </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(tag != </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
                    {
                        names.Add(tag.Val);
                    }
                    
                }
            }

            </span><span style="background: white; color: green">// Makes names unique and order by name.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">uniqueNames = names.Distinct(</span><span style="background: white; color: #2b91af">StringComparer</span><span style="background: white; color: black">.CurrentCultureIgnoreCase).OrderBy(x =&gt; x).ToList();
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">uniqueNames;
        }
    }


   
    </span><span style="background: white; color: gray">/// &lt;summary&gt;
    /// </span><span style="background: white; color: green">Code from: http://openxmldeveloper.org/blog/b/openxmldeveloper/archive/2011/04/11/137383.aspx
    </span><span style="background: white; color: gray">/// &lt;/summary&gt;
    </span><span style="background: white; color: blue">public static class </span><span style="background: white; color: #2b91af">ContentControlExtensions
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public static </span><span style="background: white; color: #2b91af">IEnumerable</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">OpenXmlElement</span><span style="background: white; color: black">&gt; ContentControls(
            </span><span style="background: white; color: blue">this </span><span style="background: white; color: #2b91af">OpenXmlPart </span><span style="background: white; color: black">part)
        {
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">part.RootElement
                .Descendants()
                .Where(e =&gt; e </span><span style="background: white; color: blue">is </span><span style="background: white; color: #2b91af">SdtBlock </span><span style="background: white; color: black">|| e </span><span style="background: white; color: blue">is </span><span style="background: white; color: #2b91af">SdtRun</span><span style="background: white; color: black">);
        }

        </span><span style="background: white; color: blue">public static </span><span style="background: white; color: #2b91af">IEnumerable</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">OpenXmlElement</span><span style="background: white; color: black">&gt; ContentControls(
            </span><span style="background: white; color: blue">this </span><span style="background: white; color: #2b91af">WordprocessingDocument </span><span style="background: white; color: black">doc)
        {
            </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">cc </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">doc.MainDocumentPart.ContentControls())
                </span><span style="background: white; color: blue">yield return </span><span style="background: white; color: black">cc;
            </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">header </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">doc.MainDocumentPart.HeaderParts)
                </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">cc </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">header.ContentControls())
                    </span><span style="background: white; color: blue">yield return </span><span style="background: white; color: black">cc;
            </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">footer </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">doc.MainDocumentPart.FooterParts)
                </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">cc </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">footer.ContentControls())
                    </span><span style="background: white; color: blue">yield return </span><span style="background: white; color: black">cc;
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(doc.MainDocumentPart.FootnotesPart != </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
                </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">cc </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">doc.MainDocumentPart.FootnotesPart.ContentControls())
                    </span><span style="background: white; color: blue">yield return </span><span style="background: white; color: black">cc;
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(doc.MainDocumentPart.EndnotesPart != </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
                </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">cc </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">doc.MainDocumentPart.EndnotesPart.ContentControls())
                    </span><span style="background: white; color: blue">yield return </span><span style="background: white; color: black">cc;
        }
    }
}
</span></pre>