---
ID: 893
post_title: 'How disabling viewstate on ASP .NET 2.0 website effects you&#8217;re code'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/29/how-disabling-viewstate-on-asp-net-2-0-website-effects-youre-code/
published: true
post_date: 2009-12-29 10:18:24
---
<p>You can disable viewstate on an ASP .NET 2.0 website by setting the enabledViewState=”false” on the configuration &gt; system.web &gt; pages node in the Web.config:    <br /><span style="color: blue">     <br />&lt;</span><span style="color: #a31515">pages </span><span style="color: red">enableViewState</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot;<span style="color: blue">&gt;</span></p> <a href="http://11011.net/software/vspaste"></a>  <p>Then you will have to fill dropdownlists etc. on every page postback in the OnInit event of the page and some times have to use the good old: this.Request.Form   <br /><span style="color: blue">     <br />string </span>selectedValue = <span style="color: blue">this</span>.Request.Form[<span style="color: #a31515">&quot;ctl00$MainContentPlaceHolder$selectBatchDropDownList&quot;</span>];    <br />The <span style="color: #a31515">&quot;ctl00$MainContentPlaceHolder$selectBatchDropDownList&quot;</span>&#160; is the control UniqueID (<strong>selectedBatchDropDownList.UniqueID</strong>)    <br />    <br />    <br /><strong>However, after reading some articles:     <br /></strong><a title="http://dotneteers.net/blogs/petersm/archive/2006/11/09/how-to-put-controlstate-into-viewstate-and-how-to-put-viewstate-into-session.aspx" href="http://dotneteers.net/blogs/petersm/archive/2006/11/09/how-to-put-controlstate-into-viewstate-and-how-to-put-viewstate-into-session.aspx">http://dotneteers.net/blogs/petersm/archive/2006/11/09/how-to-put-controlstate-into-viewstate-and-how-to-put-viewstate-into-session.aspx</a>    <br /><a title="http://weblogs.asp.net/ngur/archive/2004/03/08/85876.aspx" href="http://weblogs.asp.net/ngur/archive/2004/03/08/85876.aspx">http://weblogs.asp.net/ngur/archive/2004/03/08/85876.aspx</a>&#160; <br /><a title="http://blog.tatham.oddie.com.au/2008/12/18/how-i-learned-to-stop-worrying-and-love-the-view-state/" href="http://blog.tatham.oddie.com.au/2008/12/18/how-i-learned-to-stop-worrying-and-love-the-view-state/">http://blog.tatham.oddie.com.au/2008/12/18/how-i-learned-to-stop-worrying-and-love-the-view-state/</a>    <br />    <br />I re-enabled ViewState and started filling dropdownlists on the page “OnInit” event and saved the viewstate in the sessionstate.    <br />This allowed me to use the normal code and reduced the viewstate size to 50 characters.    <br />    <br /><strong>To persist viewstate to sessionstate use:</strong></p>  <pre class="code"><span style="color: gray">        /// &lt;summary&gt;
        /// </span><span style="color: green">Set viewstate to sessionstate
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">protected override </span><span style="color: #2b91af">PageStatePersister </span>PageStatePersister
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">return new </span><span style="color: #2b91af">SessionPageStatePersister</span>(<span style="color: blue">this</span>);
            }
        }</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>In the web.config</p>

<pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">system.web</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">browserCaps</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">case</span><span style="color: blue">&gt;
              </span>RequiresControlStateInSession=true
          <span style="color: blue">&lt;/</span><span style="color: #a31515">case</span><span style="color: blue">&gt;
      &lt;/</span><span style="color: #a31515">browserCaps</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>
  <br /><strong>To completely remove viewstate information use:</strong></p>

<pre class="code"><span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Completly disable viewstate for performance
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;viewState&quot;&gt;&lt;/param&gt;
        </span><span style="color: blue">protected override void </span>SavePageStateToPersistenceMedium(<span style="color: blue">object </span>viewState)
        {
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Completly disable viewstate  for performance
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color: blue">protected override object </span>LoadPageStateFromPersistenceMedium()
        {
            <span style="color: blue">return null</span>;
        }</pre>
<a href="http://11011.net/software/vspaste"></a>