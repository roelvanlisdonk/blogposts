---
ID: 4314
post_title: 'How to send a free SMS from C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/04/10/how-to-send-a-free-sms-from-c/
published: true
post_date: 2015-04-10 11:20:27
---
<p>I used the following code to send a free SMS from C#, by using the messagebird REST service.</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Net.Http;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Net.Http.Headers;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Threading.Tasks;

</span><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">DocumentenService.Client
{
</span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Program
</span><span style="background: white; color: black">{
</span><span style="background: white; color: blue">public static void </span><span style="background: white; color: black">Main(</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">[] args)
{
    SendSms().Wait();

    </span><span style="background: white; color: green">// Wait for the user to close this application.
    </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(</span><span style="background: white; color: #a31515">&quot;Press enter to close this application.&quot;</span><span style="background: white; color: black">);
    </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">result = </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.ReadLine();
}

</span><span style="background: white; color: gray">/// &lt;summary&gt;
/// </span><span style="background: white; color: green">Send a sms
</span><span style="background: white; color: gray">/// &lt;/summary&gt;
/// &lt;returns&gt;&lt;/returns&gt;
</span><span style="background: white; color: blue">public static async </span><span style="background: white; color: #2b91af">Task </span><span style="background: white; color: black">SendSms()
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">client = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">HttpClient</span><span style="background: white; color: black">())
    {
        client.BaseAddress = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Uri</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;https://rest.messagebird.com/&quot;</span><span style="background: white; color: black">);
        client.DefaultRequestHeaders.Accept.Clear();
        client.DefaultRequestHeaders.Accept.Add(</span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">MediaTypeWithQualityHeaderValue</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;application/json&quot;</span><span style="background: white; color: black">));
        client.DefaultRequestHeaders.Authorization = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">AuthenticationHeaderValue</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;AccessKey&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;live_...&quot;</span><span style="background: white; color: black">);
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">message = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">SmsMessage
        </span><span style="background: white; color: black">{
            body = </span><span style="background: white; color: #a31515">&quot;SMS send from C#, greetings Roel.&quot;</span><span style="background: white; color: black">,
            originator = 31611111111, </span><span style="background: white; color: green">// Sender
            </span><span style="background: white; color: black">recipients = </span><span style="background: white; color: blue">new long</span><span style="background: white; color: black">[] { 31622222222 } </span><span style="background: white; color: green">// Receivers
        </span><span style="background: white; color: black">};

        </span><span style="background: white; color: #2b91af">HttpResponseMessage </span><span style="background: white; color: black">response = </span><span style="background: white; color: blue">await </span><span style="background: white; color: black">client.PostAsJsonAsync(</span><span style="background: white; color: #a31515">&quot;messages&quot;</span><span style="background: white; color: black">, message);
        </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(response.IsSuccessStatusCode)
        {
            </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(</span><span style="background: white; color: #a31515">&quot;succes!&quot;</span><span style="background: white; color: black">);
        }
    }
}
}

</span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">SmsMessage
</span><span style="background: white; color: black">{
</span><span style="background: white; color: gray">/// &lt;summary&gt;
/// </span><span style="background: white; color: green">Example: This is a test message.
</span><span style="background: white; color: gray">/// &lt;/summary&gt;
</span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">body { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
</span><span style="background: white; color: gray">/// &lt;summary&gt;
/// </span><span style="background: white; color: green">Example: 31611111111
</span><span style="background: white; color: gray">/// &lt;/summary&gt;
</span><span style="background: white; color: blue">public long </span><span style="background: white; color: black">originator { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
</span><span style="background: white; color: gray">/// &lt;summary&gt;
/// </span><span style="background: white; color: green">Example: new long[] { 31622222222 } 
</span><span style="background: white; color: gray">/// &lt;/summary&gt;
</span><span style="background: white; color: blue">public long</span><span style="background: white; color: black">[] recipients { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
}
}
</span></pre>