---
ID: 2945
post_title: 'How to run tasks synchronously without blocking the UI thread in C# &lt;= .NET 4.0'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/11/16/how-to-run-task-synchronously-without-blocking-the-ui-thread-in-c-net-4-0/
published: true
post_date: 2012-11-16 12:06:28
---
<p>If you want to execute 3 tasks synchronously (one after the other), but you don’t want these tasks to block the UI thread. You can use the following code:</p>  <p>Note: Thread.Sleep(…) is a blocking operation and is used to mimic workload.</p>  <pre class="code"><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Threading;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Threading.Tasks;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;

</span><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">UnitTests
{
[</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
</span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">RliTests
</span><span style="background: white; color: black">{

</span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">DoWork1()
{
    </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(
        </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;DoWork1 started at [{0}] on Thread [{1}].&quot;</span><span style="background: white; color: black">, 
        </span><span style="background: white; color: #2b91af">DateTime</span><span style="background: white; color: black">.Now.ToString(</span><span style="background: white; color: #a31515">&quot;yyy-MM-dd HH:mm:ss.fff&quot;</span><span style="background: white; color: black">), 
        </span><span style="background: white; color: #2b91af">Thread</span><span style="background: white; color: black">.CurrentThread.ManagedThreadId));
    </span><span style="background: white; color: #2b91af">Thread</span><span style="background: white; color: black">.Sleep(1000);
    </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(
        </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;DoWork1 completed at [{0}] on Thread [{1}].&quot;</span><span style="background: white; color: black">, 
        </span><span style="background: white; color: #2b91af">DateTime</span><span style="background: white; color: black">.Now.ToString(</span><span style="background: white; color: #a31515">&quot;yyy-MM-dd HH:mm:ss.fff&quot;</span><span style="background: white; color: black">), 
        </span><span style="background: white; color: #2b91af">Thread</span><span style="background: white; color: black">.CurrentThread.ManagedThreadId));
}

</span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">DoWork2()
{
    </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(
        </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;DoWork2 started at [{0}] on Thread [{1}].&quot;</span><span style="background: white; color: black">, 
        </span><span style="background: white; color: #2b91af">DateTime</span><span style="background: white; color: black">.Now.ToString(</span><span style="background: white; color: #a31515">&quot;yyy-MM-dd HH:mm:ss.fff&quot;</span><span style="background: white; color: black">), 
        </span><span style="background: white; color: #2b91af">Thread</span><span style="background: white; color: black">.CurrentThread.ManagedThreadId));
    </span><span style="background: white; color: #2b91af">Thread</span><span style="background: white; color: black">.Sleep(2000);
    </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(
        </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;DoWork2 completed at [{0}] on Thread [{1}].&quot;</span><span style="background: white; color: black">, 
        </span><span style="background: white; color: #2b91af">DateTime</span><span style="background: white; color: black">.Now.ToString(</span><span style="background: white; color: #a31515">&quot;yyy-MM-dd HH:mm:ss.fff&quot;</span><span style="background: white; color: black">), 
        </span><span style="background: white; color: #2b91af">Thread</span><span style="background: white; color: black">.CurrentThread.ManagedThreadId));
}

</span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">DoWork3()
{
    </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(
        </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;DoWork3 started at [{0}] on Thread [{1}].&quot;</span><span style="background: white; color: black">, 
        </span><span style="background: white; color: #2b91af">DateTime</span><span style="background: white; color: black">.Now.ToString(</span><span style="background: white; color: #a31515">&quot;yyy-MM-dd HH:mm:ss.fff&quot;</span><span style="background: white; color: black">), 
        </span><span style="background: white; color: #2b91af">Thread</span><span style="background: white; color: black">.CurrentThread.ManagedThreadId));
    </span><span style="background: white; color: #2b91af">Thread</span><span style="background: white; color: black">.Sleep(3000);
    </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(
        </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;DoWork3 completed at [{0}] on Thread [{1}].&quot;</span><span style="background: white; color: black">, 
        </span><span style="background: white; color: #2b91af">DateTime</span><span style="background: white; color: black">.Now.ToString(</span><span style="background: white; color: #a31515">&quot;yyy-MM-dd HH:mm:ss.fff&quot;</span><span style="background: white; color: black">), 
        </span><span style="background: white; color: #2b91af">Thread</span><span style="background: white; color: black">.CurrentThread.ManagedThreadId));
}

</span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">DoWorkOnUiTrhead()
{
    </span><span style="background: white; color: blue">for </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">int </span><span style="background: white; color: black">i = 0; i &lt; 10; i++)
    {
        </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(
            </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;DoWorkOnUiTrhead started at [{0}] on Thread [{1}].&quot;</span><span style="background: white; color: black">, 
            </span><span style="background: white; color: #2b91af">DateTime</span><span style="background: white; color: black">.Now.ToString(</span><span style="background: white; color: #a31515">&quot;yyy-MM-dd HH:mm:ss.fff&quot;</span><span style="background: white; color: black">), 
            </span><span style="background: white; color: #2b91af">Thread</span><span style="background: white; color: black">.CurrentThread.ManagedThreadId));
        </span><span style="background: white; color: #2b91af">Thread</span><span style="background: white; color: black">.Sleep(1000);
        </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(
            </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;DoWorkOnUiTrhead completed at [{0}] on Thread [{1}].&quot;</span><span style="background: white; color: black">, 
            </span><span style="background: white; color: #2b91af">DateTime</span><span style="background: white; color: black">.Now.ToString(</span><span style="background: white; color: #a31515">&quot;yyy-MM-dd HH:mm:ss.fff&quot;</span><span style="background: white; color: black">), 
            </span><span style="background: white; color: #2b91af">Thread</span><span style="background: white; color: black">.CurrentThread.ManagedThreadId));
    }
}

</span><span style="background: white; color: gray">/// &lt;summary&gt;
/// </span><span style="background: white; color: green">Executing a list of tasks synchronously, without blocking the UI.
</span><span style="background: white; color: gray">/// &lt;/summary&gt;
</span><span style="background: white; color: black">[</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
</span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Test()
{
    </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(
        </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;UI ThreadId [{0}]&quot;</span><span style="background: white; color: black">,
        </span><span style="background: white; color: #2b91af">Thread</span><span style="background: white; color: black">.CurrentThread.ManagedThreadId));

    </span><span style="background: white; color: green">// Run task synchronously, but on an other thread, 
    // so the UI thread is not blocked.
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">taskAsync = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Task
     </span><span style="background: white; color: black">(
        RunTaskSyncrhonously, 
        System.Threading.Tasks.</span><span style="background: white; color: #2b91af">TaskCreationOptions</span><span style="background: white; color: black">.LongRunning
     );
    taskAsync.Start();

    </span><span style="background: white; color: green">// Execute work in the UI thread, to prove the UI is not blocked.
    </span><span style="background: white; color: black">DoWorkOnUiTrhead();
}

</span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">RunTaskSyncrhonously()
{
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">tasks = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Task</span><span style="background: white; color: black">&gt;
    {
        </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Task</span><span style="background: white; color: black">(DoWork1, 
            System.Threading.Tasks.</span><span style="background: white; color: #2b91af">TaskCreationOptions</span><span style="background: white; color: black">.LongRunning),
        </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Task</span><span style="background: white; color: black">(DoWork2, 
            System.Threading.Tasks.</span><span style="background: white; color: #2b91af">TaskCreationOptions</span><span style="background: white; color: black">.LongRunning),
        </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Task</span><span style="background: white; color: black">(DoWork3, 
            System.Threading.Tasks.</span><span style="background: white; color: #2b91af">TaskCreationOptions</span><span style="background: white; color: black">.LongRunning)
    };

    </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">Task </span><span style="background: white; color: black">task </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">tasks)
    {
        task.RunSynchronously(</span><span style="background: white; color: #2b91af">TaskScheduler</span><span style="background: white; color: black">.Default);
    }
}
}
}

</span></pre>

<p><strong>Output</strong></p>

<p>As you can see in the output, the tasks are run on an other thread, so they don’t block the UI thread, but they are run synchronously (one after the other).</p>

<p>&#160; <br />UI ThreadId [17]

  <br />DoWorkOnUiTrhead started at [2012-11-16 11:55:59.116] on Thread [17].

  <br />DoWork1 started at [2012-11-16 11:55:59.116] on Thread [18].

  <br />DoWorkOnUiTrhead completed at [2012-11-16 11:56:00.116] on Thread [17].

  <br />DoWorkOnUiTrhead started at [2012-11-16 11:56:00.116] on Thread [17].

  <br />DoWork1 completed at [2012-11-16 11:56:00.117] on Thread [18].

  <br />DoWork2 started at [2012-11-16 11:56:00.117] on Thread [18].

  <br />DoWorkOnUiTrhead completed at [2012-11-16 11:56:01.117] on Thread [17].

  <br />DoWorkOnUiTrhead started at [2012-11-16 11:56:01.117] on Thread [17].

  <br />DoWorkOnUiTrhead completed at [2012-11-16 11:56:02.117] on Thread [17].

  <br />DoWorkOnUiTrhead started at [2012-11-16 11:56:02.117] on Thread [17].

  <br />DoWork2 completed at [2012-11-16 11:56:02.118] on Thread [18].

  <br />DoWork3 started at [2012-11-16 11:56:02.118] on Thread [18].

  <br />DoWorkOnUiTrhead completed at [2012-11-16 11:56:03.118] on Thread [17].

  <br />DoWorkOnUiTrhead started at [2012-11-16 11:56:03.118] on Thread [17].

  <br />DoWorkOnUiTrhead completed at [2012-11-16 11:56:04.118] on Thread [17].

  <br />DoWorkOnUiTrhead started at [2012-11-16 11:56:04.118] on Thread [17].

  <br />DoWorkOnUiTrhead completed at [2012-11-16 11:56:05.118] on Thread [17].

  <br />DoWorkOnUiTrhead started at [2012-11-16 11:56:05.118] on Thread [17].

  <br />DoWork3 completed at [2012-11-16 11:56:05.119] on Thread [18].

  <br />DoWorkOnUiTrhead completed at [2012-11-16 11:56:06.119] on Thread [17].

  <br />DoWorkOnUiTrhead started at [2012-11-16 11:56:06.119] on Thread [17].

  <br />DoWorkOnUiTrhead completed at [2012-11-16 11:56:07.120] on Thread [17].

  <br />DoWorkOnUiTrhead started at [2012-11-16 11:56:07.120] on Thread [17].

  <br />DoWorkOnUiTrhead completed at [2012-11-16 11:56:08.120] on Thread [17].

  <br />DoWorkOnUiTrhead started at [2012-11-16 11:56:08.120] on Thread [17].

  <br />DoWorkOnUiTrhead completed at [2012-11-16 11:56:09.120] on Thread [17].</p>