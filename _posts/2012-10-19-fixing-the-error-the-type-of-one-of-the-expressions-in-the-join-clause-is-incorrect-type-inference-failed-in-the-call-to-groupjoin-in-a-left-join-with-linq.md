---
ID: 2904
post_title: 'Fixing the error: The type of one of the expressions in the join clause is incorrect.  Type inference failed in the call to &#8216;GroupJoin&#8217;. in a left join with LINQ.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/10/19/fixing-the-error-the-type-of-one-of-the-expressions-in-the-join-clause-is-incorrect-type-inference-failed-in-the-call-to-groupjoin-in-a-left-join-with-linq/
published: true
post_date: 2012-10-19 09:17:38
---
<p>If you do a left join in LINQ on multiple columns / properties. The types and names of these properties must be the same else you will get the error:</p>  <p>The type of one of the expressions in the join clause is incorrect.&#160; Type inference failed in the call to 'GroupJoin'.</p>  <p>&#160;</p>  <p>The following code generates the error, because the property [Company] is not the exact same as the property [Comp]. </p>  <pre class="code"><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: #2b91af">Assert </span><span style="background: white; color: black">= Xunit.</span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">;

</span><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.Rli.Tests
{
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Person1
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Name { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Company { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    }

    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Person2
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Name { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Comp { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    }


    [</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">ResearchTester
    </span><span style="background: white; color: black">{
        [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Should_join_person1_and_person2()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">p1List = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Person1</span><span style="background: white; color: black">&gt;
            {
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Person1 </span><span style="background: white; color: black">{ Company = </span><span style="background: white; color: #a31515">&quot;MyCompany&quot;</span><span style="background: white; color: black">, Name = </span><span style="background: white; color: #a31515">&quot;John Do&quot;</span><span style="background: white; color: black">}
            };

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">p2List = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Person2</span><span style="background: white; color: black">&gt;
            {
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Person2 </span><span style="background: white; color: black">{ Comp = </span><span style="background: white; color: #a31515">&quot;MyCompany&quot;</span><span style="background: white; color: black">, Name = </span><span style="background: white; color: #a31515">&quot;John Do&quot;</span><span style="background: white; color: black">}
            };



            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">query = </span><span style="background: white; color: blue">from </span><span style="background: white; color: black">p1 </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">p1List
                        </span><span style="background: white; color: blue">join </span><span style="background: white; color: black">p2 </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">p2List </span><span style="background: white; color: blue">on new </span><span style="background: white; color: black">{ p1.Company, p1.Name } </span><span style="background: white; color: blue">equals new </span><span style="background: white; color: black">{ p2.Comp, p2.Name } </span><span style="background: white; color: blue">into </span><span style="background: white; color: black">p2g
                        </span><span style="background: white; color: blue">from </span><span style="background: white; color: black">p2g1 </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">p2g.DefaultIfEmpty(</span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
                        </span><span style="background: white; color: blue">select </span><span style="background: white; color: black">p1;
           
        }
    }
}


</span></pre>


<p>To fix this error add property names to the anonymous objects.</p>

<pre class="code"><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: #2b91af">Assert </span><span style="background: white; color: black">= Xunit.</span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">;

</span><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.Rli.Tests
{
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Person1
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Name { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Company { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    }

    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Person2
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Name { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Comp { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    }


    [</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">ResearchTester
    </span><span style="background: white; color: black">{
        [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Should_join_person1_and_person2()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">p1List = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Person1</span><span style="background: white; color: black">&gt;
            {
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Person1 </span><span style="background: white; color: black">{ Company = </span><span style="background: white; color: #a31515">&quot;MyCompany&quot;</span><span style="background: white; color: black">, Name = </span><span style="background: white; color: #a31515">&quot;John Do&quot;</span><span style="background: white; color: black">}
            };

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">p2List = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Person2</span><span style="background: white; color: black">&gt;
            {
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Person2 </span><span style="background: white; color: black">{ Comp = </span><span style="background: white; color: #a31515">&quot;MyCompany&quot;</span><span style="background: white; color: black">, Name = </span><span style="background: white; color: #a31515">&quot;John Do&quot;</span><span style="background: white; color: black">}
            };



            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">query = </span><span style="background: white; color: blue">from </span><span style="background: white; color: black">p1 </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">p1List
                        </span><span style="background: white; color: blue">join </span><span style="background: white; color: black">p2 </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">p2List </span><span style="background: white; color: blue">on new </span><span style="background: white; color: black">{ Company = p1.Company, Name = p1.Name } <br />                        </span><span style="background: white; color: blue">equals new </span><span style="background: white; color: black">{ Company = p2.Comp, Name = p2.Name } </span><span style="background: white; color: blue">into </span><span style="background: white; color: black">p2g
                        </span><span style="background: white; color: blue">from </span><span style="background: white; color: black">p2g1 </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">p2g.DefaultIfEmpty(</span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
                        </span><span style="background: white; color: blue">select </span><span style="background: white; color: black">p1;
           
        }
    }
}


</span></pre>