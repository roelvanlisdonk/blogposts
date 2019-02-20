---
ID: 3764
post_title: >
  JavaScript private, public, shared and
  instance variables with IIFE.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/05/14/javascript-private-public-shared-and-instance-variables/
published: true
post_date: 2014-05-14 22:09:55
---
<p>Just a reminder, when using a Immediately-Invoked Function Expression (IIFE), you can create private, public, shared and instance variables:</p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Show public - private - shared and instance variables.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
        var </span><span style="background: white; color: black">Greeter = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">v1 = 10; </span><span style="background: white; color: green">// This is a private variable shared by all instances of Greeter.

            </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">Greeter(name)
            {
                </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">.name = name;
                </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">.v2 = 20; </span><span style="background: white; color: green">// This is a public instance variable.
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">v3 = 30; </span><span style="background: white; color: green">// This is a private instance variable, can only be <br />                             // accessed by the current Greeter instance.
            </span><span style="background: white; color: black">}

            Greeter.prototype.v4 = 40; </span><span style="background: white; color: green">// This is a public variable shared by all instances of Greeter.

            </span><span style="background: white; color: black">Greeter.prototype.increase = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
            {
                v1 = v1 + 1;
                </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">.v2 = </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">.v2 + 1;
            };


            Greeter.prototype.logState = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
            {
                console.log(</span><span style="background: white; color: blue">this</span><span style="background: white; color: black">.name + </span><span style="background: white; color: #a31515">&quot;.v1 [&quot; </span><span style="background: white; color: black">+ v1.toString() + </span><span style="background: white; color: #a31515">&quot;]&quot; </span><span style="background: white; color: black">+ <br />                            </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">.name + </span><span style="background: white; color: #a31515">&quot;.v2 [&quot; </span><span style="background: white; color: black">+ </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">.v2.toString() + </span><span style="background: white; color: #a31515">&quot;].&quot;</span><span style="background: white; color: black">);
            };

            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">Greeter;
        })();

        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">greeter1 = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">Greeter(</span><span style="background: white; color: #a31515">&quot;greeter1&quot;</span><span style="background: white; color: black">);
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">greeter2 = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">Greeter(</span><span style="background: white; color: #a31515">&quot;greeter2&quot;</span><span style="background: white; color: black">);

        greeter1.logState(); </span><span style="background: white; color: green">// Logs: greeter1.v1 [10] greeter1.v2 [20].
        </span><span style="background: white; color: black">greeter2.logState(); </span><span style="background: white; color: green">// Logs: greeter1.v1 [10] greeter1.v2 [20].

        </span><span style="background: white; color: black">greeter1.increase();

        greeter1.logState(); </span><span style="background: white; color: green">// Logs: greeter1.v1 [11] greeter1.v2 [21].
        </span><span style="background: white; color: black">greeter2.logState(); </span><span style="background: white; color: green">// Logs: greeter1.v1 [11] greeter1.v2 [20].
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></pre>