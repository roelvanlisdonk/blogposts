---
ID: 3531
post_title: 'How to dynamically bind data to Content Controls in a Microsoft Word document by using OpenXml and C#.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/11/03/how-to-dynamically-bind-data-to-content-controls-in-a-microsoft-word-document-by-using-openxml-and-c/
published: true
post_date: 2013-11-03 22:01:43
---
<p>&#160;</p>  <p>Create a new Microsoft Word document add two content controls with the names:</p>  <ul>   <li>Employee_Firstname</li>    <li>Employee_Lastname </li> </ul>  <p>Like:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image_thumb.png" width="580" height="330" /></a></p>  <p>&#160;</p>  <p>Employee_Lastname</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image_thumb1.png" width="580" height="326" /></a></p>  <p>&#160;</p>  <p>Now when you run the unittest below, the following the result will be:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image2.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image_thumb2.png" width="244" height="188" /></a></p>  <p>&#160;</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">EndToEndTest
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">DocumentFormat.OpenXml;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">DocumentFormat.OpenXml.CustomXmlDataProperties;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">DocumentFormat.OpenXml.Packaging;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">DocumentFormat.OpenXml.Wordprocessing;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.IO;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Xml;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Xml.Linq;

    [</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">RliResearch
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">private </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt; _tagNames = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt;();
        </span><span style="background: white; color: blue">private </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt; _uniqueTagNames = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt;();

        [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Test_with_duration()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">watch = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">System.Diagnostics.</span><span style="background: white; color: #2b91af">Stopwatch</span><span style="background: white; color: black">();
            watch.Start();

            InitialiseDatabinding();

            watch.Stop();
            System.</span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(watch.Elapsed.TotalMilliseconds);
        }

        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">InitialiseDatabinding()
        {
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">WordprocessingDocument </span><span style="background: white; color: black">doc = </span><span style="background: white; color: #2b91af">WordprocessingDocument</span><span style="background: white; color: black">.Open(</span><span style="background: white; color: #a31515">@&quot;C:\Temp\Test.docx&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">))
            {
                
                </span><span style="background: white; color: #2b91af">CustomXmlPart </span><span style="background: white; color: black">customXmlPart = doc.MainDocumentPart.CustomXmlParts.FirstOrDefault();
                </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(customXmlPart == </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
                {
                    customXmlPart = doc.MainDocumentPart.AddCustomXmlPart(</span><span style="background: white; color: #2b91af">CustomXmlPartType</span><span style="background: white; color: black">.CustomXml);
                }

                </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(customXmlPart.CustomXmlPropertiesPart == </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
                {
                    customXmlPart.AddNewPart&lt;</span><span style="background: white; color: #2b91af">CustomXmlPropertiesPart</span><span style="background: white; color: black">&gt;();
                }

                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">propertiesPart = customXmlPart.CustomXmlPropertiesPart;

                </span><span style="background: white; color: blue">if</span><span style="background: white; color: black">(propertiesPart.DataStoreItem == </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
                {
                    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">dataStoreItem = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">DataStoreItem</span><span style="background: white; color: black">() { ItemId = </span><span style="background: white; color: #2b91af">Guid</span><span style="background: white; color: black">.NewGuid().ToString(</span><span style="background: white; color: #a31515">&quot;B&quot;</span><span style="background: white; color: black">) };
                    propertiesPart.DataStoreItem = dataStoreItem;
                }

                </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">dataStoreId = customXmlPart.CustomXmlPropertiesPart.DataStoreItem.ItemId;

                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">names = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt;();

                </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">cc </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">doc.ContentControls())
                {
                    </span><span style="background: white; color: #2b91af">SdtProperties </span><span style="background: white; color: black">props = cc.Elements&lt;</span><span style="background: white; color: #2b91af">SdtProperties</span><span style="background: white; color: black">&gt;().FirstOrDefault();
                    </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(props != </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
                    {
                        </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">name = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Empty;
                        </span><span style="background: white; color: blue">try
                        </span><span style="background: white; color: black">{
                            </span><span style="background: white; color: #2b91af">Tag </span><span style="background: white; color: black">tag = props.Elements&lt;</span><span style="background: white; color: #2b91af">Tag</span><span style="background: white; color: black">&gt;().FirstOrDefault();
                            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(tag != </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
                            {
                                name = tag.Val.ToString();
                                names.Add(name);
                                tag.Val = name;

                                DocumentFormat.OpenXml.Wordprocessing.</span><span style="background: white; color: #2b91af">SdtAlias </span><span style="background: white; color: black">alias = props.Elements&lt;DocumentFormat.OpenXml.Wordprocessing.</span><span style="background: white; color: #2b91af">SdtAlias</span><span style="background: white; color: black">&gt;().FirstOrDefault();
                                </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(alias != </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
                                {
                                    alias.Val = name;
                                }

                                </span><span style="background: white; color: green">// Update databinding
                                </span><span style="background: white; color: black">DocumentFormat.OpenXml.Wordprocessing.</span><span style="background: white; color: #2b91af">DataBinding </span><span style="background: white; color: black">dataBinding = props.Elements&lt;DocumentFormat.OpenXml.Wordprocessing.</span><span style="background: white; color: #2b91af">DataBinding</span><span style="background: white; color: black">&gt;().FirstOrDefault();
                                </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(dataBinding == </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
                                {
                                    dataBinding = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">DataBinding</span><span style="background: white; color: black">();
                                    dataBinding.XPath = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;/Root[1]/{0}[1]&quot;</span><span style="background: white; color: black">, name);
                                    dataBinding.StoreItemId = dataStoreId;
                                    props.Append(dataBinding);
                                }
                                </span><span style="background: white; color: blue">else
                                </span><span style="background: white; color: black">{
                                    dataBinding.XPath = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;/Root[1]/{0}[1]&quot;</span><span style="background: white; color: black">, name);
                                    dataBinding.StoreItemId = dataStoreId;
                                }
                            }
                        }
                        </span><span style="background: white; color: blue">catch </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">Exception </span><span style="background: white; color: black">ex)
                        {
                            </span><span style="background: white; color: blue">throw new </span><span style="background: white; color: #2b91af">ApplicationException</span><span style="background: white; color: black">(</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;Exception found during processing of tag [{0}].&quot;</span><span style="background: white; color: black">, name), ex);
                        }
                    }
                }

                </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt; uniqueTagNames = names.Distinct(</span><span style="background: white; color: #2b91af">StringComparer</span><span style="background: white; color: black">.CurrentCultureIgnoreCase).OrderBy(x =&gt; x).ToList();

                </span><span style="background: white; color: #2b91af">XDocument </span><span style="background: white; color: black">xdoc = CreateXmlDocument(</span><span style="background: white; color: #a31515">&quot;Root&quot;</span><span style="background: white; color: black">, uniqueTagNames);

                SaveCustomXmlPart(customXmlPart, xdoc);
            }
        }

        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Create a XDocument, with a root element based on the given &quot;rootName&quot;, containing child elements based on the given &quot;tagnames&quot;.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">XDocument </span><span style="background: white; color: black">CreateXmlDocument(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">rootName, </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt; tagNames)
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">document = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">XDocument</span><span style="background: white; color: black">(
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">XDeclaration</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;1.0&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;utf-8&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">),
                    </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">XElement</span><span style="background: white; color: black">(rootName,
                        tagNames.Select(x =&gt; 
                        {
                            </span><span style="background: white; color: #2b91af">XElement </span><span style="background: white; color: black">xe = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">XElement</span><span style="background: white; color: black">(x, </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Empty);
                            </span><span style="background: white; color: blue">if</span><span style="background: white; color: black">(</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Compare(x, </span><span style="background: white; color: #a31515">&quot;Employee_Firstname&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">) == 0)
                            {
                               xe = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">XElement</span><span style="background: white; color: black">(x, </span><span style="background: white; color: #a31515">&quot;Johny&quot;</span><span style="background: white; color: black">);
                            }
                            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Compare(x, </span><span style="background: white; color: #a31515">&quot;Employee_Lastname&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">) == 0)
                            {
                               xe= </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">XElement</span><span style="background: white; color: black">(x, </span><span style="background: white; color: #a31515">&quot;Droptables&quot;</span><span style="background: white; color: black">);
                            }
                            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">xe;
                        }
                    )
                )
            );

            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">document;
        }

        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">SaveCustomXmlPart(</span><span style="background: white; color: #2b91af">CustomXmlPart </span><span style="background: white; color: black">part, </span><span style="background: white; color: #2b91af">XDocument </span><span style="background: white; color: black">xdoc)
        {
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">stream = part.GetStream(</span><span style="background: white; color: #2b91af">FileMode</span><span style="background: white; color: black">.Create, </span><span style="background: white; color: #2b91af">FileAccess</span><span style="background: white; color: black">.ReadWrite))
            {
                </span><span style="background: white; color: green">// Reset stream position to 0, to prevent errors.
                </span><span style="background: white; color: black">stream.Position = 0;

                </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">XmlWriter </span><span style="background: white; color: black">xw = </span><span style="background: white; color: #2b91af">XmlWriter</span><span style="background: white; color: black">.Create(stream))
                {
                    xdoc.Save(xw);
                }
            }
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