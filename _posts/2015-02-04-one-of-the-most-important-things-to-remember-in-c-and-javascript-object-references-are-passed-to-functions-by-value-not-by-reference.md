---
ID: 4267
post_title: 'One of the most important things to remember: In C# and JavaScript, object references are passed to functions by value not by reference'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/02/04/one-of-the-most-important-things-to-remember-in-c-and-javascript-object-references-are-passed-to-functions-by-value-not-by-reference/
published: true
post_date: 2015-02-04 09:34:29
---
<p>By default C# and JavaScript pass object references by value not by reference, but what does that mean?</p>  <p>Well if you assign an object to a variable, this variable is just a pointer to that object in memory.</p>  <p>(Examples in C#)</p>   <pre class="code"><span style="background: white; color: blue">var </span><span style="background: white; color: black">person = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Person
            </span><span style="background: white; color: black">{
                Id = 2,
                Name = </span><span style="background: white; color: #a31515">&quot;John&quot;
            </span><span style="background: white; color: black">};</span></pre>
The variable person is just a pointer to the object in memory, the memory contains the object { Id = 2, Name = “John”}

<p>When passed to a function, a copy of this pointer is supplied to the function, not the object itself.</p>

<p>So when you update properties of the object in the function, the variable outside the function will get updated.</p>

<p>&#160;</p>

<p><strong><font size="4">But when you set the object to NULL in the function, the variable outside the function will <font color="#c0504d">NOT</font> be set to NULL.</font></strong></p>

<p>&#160;</p>

<p>In C# you can override this by adding the “ref” keyword before the parameter, in that case the pointer of the variable will be passed and thus setting the object to null in the function will set the variable outside the function to NULL.</p>

<p>&#160;</p>

<p>Some unit test to explain this:</p>

<pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Test
{
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;      

[</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
</span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Research
</span><span style="background: white; color: black">{

[</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
</span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Update_object_properties_should_update_variable()
{

    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">person = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Person
    </span><span style="background: white; color: black">{
        Id = 2,
        Name = </span><span style="background: white; color: #a31515">&quot;John&quot;
    </span><span style="background: white; color: black">};

    UpdateObjectProperties(person);

    </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.IsTrue(person.Name == </span><span style="background: white; color: #a31515">&quot;Mike&quot;</span><span style="background: white; color: black">);
}

</span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">UpdateObjectProperties(</span><span style="background: white; color: #2b91af">Person </span><span style="background: white; color: black">person)
{
    person.Name = </span><span style="background: white; color: #a31515">&quot;Mike&quot;</span><span style="background: white; color: black">;
}

[</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
</span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Update_object_pointer_should_not_update_variable()
{

    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">person = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Person
    </span><span style="background: white; color: black">{
        Id = 2,
        Name = </span><span style="background: white; color: #a31515">&quot;John&quot;
    </span><span style="background: white; color: black">};

    UpdateObjectPointer(person);

    </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.IsTrue(person.Name == </span><span style="background: white; color: #a31515">&quot;John&quot;</span><span style="background: white; color: black">);
}

</span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">UpdateObjectPointer(</span><span style="background: white; color: #2b91af">Person </span><span style="background: white; color: black">person)
{
    person = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;
}
}

</span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Person
</span><span style="background: white; color: black">{
    </span><span style="background: white; color: blue">public int </span><span style="background: white; color: black">Id { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Name { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
}
}
</span></pre>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/02/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/02/image_thumb.png" width="580" height="595" /></a></p>

<p>&#160;</p>

<p>More info can be found at:</p>

<p><a title="http://stackoverflow.com/questions/9717057/c-sharp-passing-arguments-by-default-is-byref-instead-of-byval" href="http://stackoverflow.com/questions/9717057/c-sharp-passing-arguments-by-default-is-byref-instead-of-byval">http://stackoverflow.com/questions/9717057/c-sharp-passing-arguments-by-default-is-byref-instead-of-byval</a></p>

<p><a title="http://jonskeet.uk/csharp/parameters.html" href="http://jonskeet.uk/csharp/parameters.html">http://jonskeet.uk/csharp/parameters.html</a></p>

<p><a title="http://jonskeet.uk/csharp/references.html" href="http://jonskeet.uk/csharp/references.html">http://jonskeet.uk/csharp/references.html</a></p>