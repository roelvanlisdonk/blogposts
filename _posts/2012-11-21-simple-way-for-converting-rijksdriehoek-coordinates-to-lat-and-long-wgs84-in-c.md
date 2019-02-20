---
ID: 2950
post_title: 'Simple way for converting &quot;Rijksdriehoek&quot; coordinates to lat and long (WGS84) in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/11/21/simple-way-for-converting-rijksdriehoek-coordinates-to-lat-and-long-wgs84-in-c/
published: true
post_date: 2012-11-21 12:37:17
---
<p>In the Netherlands &quot;Rijksdriehoek&quot; coordinates are used to show the exact position of an object on a chart. To convert &quot;Rijksdriehoek&quot; coordinates to lat and long coordinates in C# use the following class:</p>  <p>&#160;</p>  <p><strong>Note</strong></p>  <p align="left">This code is base on the information found in&#160; <a title="http://www.dekoepel.nl/pdf/Transformatieformules.pdf" href="http://www.dekoepel.nl/pdf/Transformatieformules.pdf">http://www.dekoepel.nl/pdf/Transformatieformules.pdf</a></p>  <pre class="code"><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Globalization;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Text;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Threading.Tasks;

</span><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.Core
{
</span><span style="background: white; color: blue">public interface </span><span style="background: white; color: #2b91af">IRijksdriehoekComponent
</span><span style="background: white; color: black">{
</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">ConvertToLatLong(</span><span style="background: white; color: blue">double </span><span style="background: white; color: black">x, </span><span style="background: white; color: blue">double </span><span style="background: white; color: black">y);
}

</span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">RijksdriehoekComponent </span><span style="background: white; color: black">: </span><span style="background: white; color: #2b91af">IRijksdriehoekComponent
</span><span style="background: white; color: black">{
</span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">ConvertToLatLong(</span><span style="background: white; color: blue">double </span><span style="background: white; color: black">x, </span><span style="background: white; color: blue">double </span><span style="background: white; color: black">y)
{
    </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">result = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;

    </span><span style="background: white; color: green">// The city &quot;Amsterfoort&quot; is used as reference &quot;Rijksdriehoek&quot; coordinate.
    </span><span style="background: white; color: blue">int </span><span style="background: white; color: black">referenceRdX = 155000;
    </span><span style="background: white; color: blue">int </span><span style="background: white; color: black">referenceRdY = 463000;

    </span><span style="background: white; color: blue">double </span><span style="background: white; color: black">dX = (</span><span style="background: white; color: blue">double</span><span style="background: white; color: black">)(x - referenceRdX) * (</span><span style="background: white; color: blue">double</span><span style="background: white; color: black">)(</span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(10,-5));
    </span><span style="background: white; color: blue">double </span><span style="background: white; color: black">dY = (</span><span style="background: white; color: blue">double</span><span style="background: white; color: black">)(y - referenceRdY) * (</span><span style="background: white; color: blue">double</span><span style="background: white; color: black">)(</span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(10,-5));

    </span><span style="background: white; color: blue">double </span><span style="background: white; color: black">sumN = 
        (3235.65389 * dY) + 
        (-32.58297 * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dX, 2)) + 
        (-0.2475 * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dY, 2)) + 
        (-0.84978 * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dX, 2) * dY) + 
        (-0.0655 * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dY, 3)) + 
        (-0.01709 * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dX, 2) * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dY, 2)) + 
        (-0.00738 * dX) + 
        (0.0053 * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dX, 4)) + 
        (-0.00039 * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dX, 2) * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dY, 3)) + 
        (0.00033 * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dX, 4) * dY) + 
        (-0.00012 * dX * dY);
    </span><span style="background: white; color: blue">double </span><span style="background: white; color: black">sumE = 
        (5260.52916 * dX) + 
        (105.94684 * dX * dY) + 
        (2.45656 * dX * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dY, 2)) + 
        (-0.81885 * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dX, 3)) + 
        (0.05594 * dX * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dY, 3)) + 
        (-0.05607 * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dX, 3) * dY) + 
        (0.01199 * dY) + 
        (-0.00256 * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dX, 3) * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dY, 2)) + 
        (0.00128 * dX * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dY, 4)) + 
        (0.00022 * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dY, 2)) + 
        (-0.00022 * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dX, 2)) + 
        (0.00026 * </span><span style="background: white; color: #2b91af">Math</span><span style="background: white; color: black">.Pow(dX, 5));


    </span><span style="background: white; color: green">// The city &quot;Amsterfoort&quot; is used as reference &quot;WGS84&quot; coordinate.
    </span><span style="background: white; color: blue">double </span><span style="background: white; color: black">referenceWgs84X = 52.15517;
    </span><span style="background: white; color: blue">double </span><span style="background: white; color: black">referenceWgs84Y = 5.387206;

    </span><span style="background: white; color: blue">double </span><span style="background: white; color: black">latitude = referenceWgs84X + (sumN / 3600);
    </span><span style="background: white; color: blue">double </span><span style="background: white; color: black">longitude = referenceWgs84Y + (sumE / 3600);

    </span><span style="background: white; color: green">// Input
    // x = 122202
    // y = 487250
    //
    // Result
    // &quot;52.372143838117, 4.90559760435224&quot;
    </span><span style="background: white; color: black">result = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;{0}, {1}&quot;</span><span style="background: white; color: black">, 
        latitude.ToString(</span><span style="background: white; color: #2b91af">CultureInfo</span><span style="background: white; color: black">.InvariantCulture.NumberFormat),
        longitude.ToString(</span><span style="background: white; color: #2b91af">CultureInfo</span><span style="background: white; color: black">.InvariantCulture.NumberFormat));

    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">result;
}
}
}
</span></pre>


<p><strong>Test</strong></p>

<pre class="code"><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Research.Core;

</span><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">UnitTest
{
[</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
</span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">RijksdriehoekComponentTests
</span><span style="background: white; color: black">{
    [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">TestMethod1()
    {
        </span><span style="background: white; color: #2b91af">IRijksdriehoekComponent </span><span style="background: white; color: black">component = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">RijksdriehoekComponent</span><span style="background: white; color: black">();
        </span><span style="background: white; color: blue">double </span><span style="background: white; color: black">x = 122202;
        </span><span style="background: white; color: blue">double </span><span style="background: white; color: black">y = 487250;
        </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">result = component.ConvertToLatLong(x, y);
        </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.AreEqual(</span><span style="background: white; color: #a31515">&quot;52.372143838117, 4.90559760435224&quot;</span><span style="background: white; color: black">, result);
    }
}
}
</span></pre>