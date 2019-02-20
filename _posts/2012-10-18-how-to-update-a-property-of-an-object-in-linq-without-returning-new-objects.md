---
ID: 2901
post_title: >
  How to update a property of an object in
  LINQ without returning new objects.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/10/18/how-to-update-a-property-of-an-object-in-linq-without-returning-new-objects/
published: true
post_date: 2012-10-18 14:09:10
---
<p>If you want to update an property of an object in LINQ without creating new objects, you can use the following code:</p>  <pre class="code"><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: #2b91af">Assert </span><span style="background: white; color: black">= Xunit.</span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">;

</span><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.Rli.Tests
{
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Appointment
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public int </span><span style="background: white; color: black">Id { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Location { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    }

    [</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">ResearchTester
    </span><span style="background: white; color: black">{
        [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Should_update_appointments()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">appointments1 = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Appointment</span><span style="background: white; color: black">&gt;
            {
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Appointment </span><span style="background: white; color: black">{ Id = 1, Location = </span><span style="background: white; color: #a31515">&quot;&quot; </span><span style="background: white; color: black">},
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Appointment </span><span style="background: white; color: black">{ Id = 2, Location = </span><span style="background: white; color: #a31515">&quot;&quot; </span><span style="background: white; color: black">},
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Appointment </span><span style="background: white; color: black">{ Id = 3, Location = </span><span style="background: white; color: #a31515">&quot;&quot; </span><span style="background: white; color: black">}
            };

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">appointments2 = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Appointment</span><span style="background: white; color: black">&gt;
            {
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Appointment </span><span style="background: white; color: black">{ Id = 1, Location = </span><span style="background: white; color: #a31515">&quot;My location 1&quot; </span><span style="background: white; color: black">},
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Appointment </span><span style="background: white; color: black">{ Id = 2, Location = </span><span style="background: white; color: #a31515">&quot;&quot; </span><span style="background: white; color: black">},
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Appointment </span><span style="background: white; color: black">{ Id = 3, Location = </span><span style="background: white; color: #a31515">&quot;My location 3&quot; </span><span style="background: white; color: black">}
            };

            </span><span style="background: white; color: #2b91af">Func</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Appointment</span><span style="background: white; color: black">, </span><span style="background: white; color: #2b91af">Appointment</span><span style="background: white; color: black">, </span><span style="background: white; color: #2b91af">Appointment</span><span style="background: white; color: black">&gt; UpdateLocation 
                = ((a, b) =&gt; { a.Location = b.Location; </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">a; });

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">updatedAppointmets = (</span><span style="background: white; color: blue">from </span><span style="background: white; color: black">a1 </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">appointments1
                                     </span><span style="background: white; color: blue">join </span><span style="background: white; color: black">a2 </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">appointments2 </span><span style="background: white; color: blue">on </span><span style="background: white; color: black">a1.Id </span><span style="background: white; color: blue">equals </span><span style="background: white; color: black">a2.Id
                                      </span><span style="background: white; color: blue">select </span><span style="background: white; color: black">UpdateLocation(a1, a2)).ToList();

            </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">Appointment </span><span style="background: white; color: black">a </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">updatedAppointmets)
            {
                </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine
                (
                    </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;Id [{0}] Location [{1}]&quot;</span><span style="background: white; color: black">, a.Id, a.Location)
                );
            }

            </span><span style="background: white; color: green">// Output:
            // Id [1] Location [My location 1]
            // Id [2] Location []
            // Id [3] Location [My location 3]
        </span><span style="background: white; color: black">}
    }
}


</span></pre>


<p>If you want to use a LEFT OUTER JOIN in the linq query, use:</p>

<p>&#160;</p>

<pre class="code"><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: #2b91af">Assert </span><span style="background: white; color: black">= Xunit.</span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">;

</span><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.Rli.Tests
{
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Appointment
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public int </span><span style="background: white; color: black">Id { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Location { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    }

    [</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">ResearchTester
    </span><span style="background: white; color: black">{
        [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Should_update_appointments()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">appointments1 = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Appointment</span><span style="background: white; color: black">&gt;
            {
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Appointment </span><span style="background: white; color: black">{ Id = 1, Location = </span><span style="background: white; color: #a31515">&quot;&quot; </span><span style="background: white; color: black">},
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Appointment </span><span style="background: white; color: black">{ Id = 2, Location = </span><span style="background: white; color: #a31515">&quot;&quot; </span><span style="background: white; color: black">},
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Appointment </span><span style="background: white; color: black">{ Id = 3, Location = </span><span style="background: white; color: #a31515">&quot;&quot; </span><span style="background: white; color: black">}
            };

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">appointments2 = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Appointment</span><span style="background: white; color: black">&gt;
            {
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Appointment </span><span style="background: white; color: black">{ Id = 1, Location = </span><span style="background: white; color: #a31515">&quot;My location 1&quot; </span><span style="background: white; color: black">},
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Appointment </span><span style="background: white; color: black">{ Id = 3, Location = </span><span style="background: white; color: #a31515">&quot;My location 3&quot; </span><span style="background: white; color: black">}
            };

            </span><span style="background: white; color: #2b91af">Func</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Appointment</span><span style="background: white; color: black">, </span><span style="background: white; color: #2b91af">Appointment</span><span style="background: white; color: black">, </span><span style="background: white; color: #2b91af">Appointment</span><span style="background: white; color: black">&gt; UpdateLocation
                = ((a, b) =&gt; { </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(b != </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">) { a.Location = b.Location; } </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">a; });

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">updatedAppointmets =
            (
                </span><span style="background: white; color: blue">from </span><span style="background: white; color: black">a1 </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">appointments1
                </span><span style="background: white; color: blue">join </span><span style="background: white; color: black">a2 </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">appointments2 </span><span style="background: white; color: blue">on </span><span style="background: white; color: black">a1.Id </span><span style="background: white; color: blue">equals </span><span style="background: white; color: black">a2.Id </span><span style="background: white; color: blue">into </span><span style="background: white; color: black">g
                </span><span style="background: white; color: blue">from </span><span style="background: white; color: black">g1 </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">g.DefaultIfEmpty(</span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
                </span><span style="background: white; color: blue">select </span><span style="background: white; color: black">UpdateLocation(a1, g1)
            ).ToList();

            </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">Appointment </span><span style="background: white; color: black">a </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">updatedAppointmets)
            {
                </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine
                (
                    </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;Id [{0}] Location [{1}]&quot;</span><span style="background: white; color: black">, a.Id, a.Location)
                );
            }

            </span><span style="background: white; color: green">// Output:
            // Id [1] Location [My location 1]
            // Id [2] Location []
            // Id [3] Location [My location 3]
        </span><span style="background: white; color: black">}
    }
}


</span></pre>