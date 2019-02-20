---
ID: 3599
post_title: 'How to change Application scope Settings (that are read-only) at runtime in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/12/11/how-to-change-application-scope-settings-that-are-read-only-at-runtime-in-c/
published: true
post_date: 2013-12-11 08:19:20
---
<p>If you set your settings to the &quot;Application&quot; scope the settings will be read-only.</p>  <p>If you want to change these settings at runtime, you can use the following code from my unit test project:</p>  <p>&#160;</p>  <p>First create a Settings class in your unit test project:</p>  <p>Right click on the unit test project and choose &quot;Properties&quot;.</p>  <p>Click on &quot;Settings&quot;:</p>  <p>Click on &quot;This project does not contain a default settings file. Click here to create one.&quot;</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/12/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/12/image_thumb.png" width="511" height="245" /></a></p>  <p>&#160;</p>  <p>At two test settings: &quot;MyStringSetting&quot; and &quot;MyInSetting&quot;&quot;:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/12/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/12/image_thumb1.png" width="580" height="184" /></a></p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/12/image2.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/12/image_thumb2.png" width="244" height="169" /></a></p>  <p>&#160;</p>  <p>The App.config will be changed like:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/12/image3.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/12/image_thumb3.png" width="580" height="172" /></a></p>  <p>&#160;</p>  <p>Now to show the code that changes the settings at runtime:</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">UnitTestProject2
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">UnitTestProject2.Properties;

    [</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">UnitTest1
    </span><span style="background: white; color: black">{
        [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">TestMethod1()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">settings = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Settings</span><span style="background: white; color: black">();
            
            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.AreEqual(settings.MyStringSetting, </span><span style="background: white; color: #a31515">&quot;This is some random text.&quot;</span><span style="background: white; color: black">);
            settings.ChangeSetting(</span><span style="background: white; color: #a31515">&quot;MyStringSetting&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;This is some other text.&quot;</span><span style="background: white; color: black">);
            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.AreEqual(settings.MyStringSetting, </span><span style="background: white; color: #a31515">&quot;This is some other text.&quot;</span><span style="background: white; color: black">);

            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.AreEqual(settings.MyIntSetting, 999);
            settings.ChangeSetting(</span><span style="background: white; color: #a31515">&quot;MyIntSetting&quot;</span><span style="background: white; color: black">, 100);
            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.AreEqual(settings.MyIntSetting, 100);
        }
    }
    
}

</span><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">UnitTestProject2.Properties
{
    </span><span style="background: white; color: blue">internal sealed partial class </span><span style="background: white; color: #2b91af">Settings
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">ChangeSetting&lt;T&gt;(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">key, T value)
        {
            </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">[key] = value;
        }
    }
}</span></pre>