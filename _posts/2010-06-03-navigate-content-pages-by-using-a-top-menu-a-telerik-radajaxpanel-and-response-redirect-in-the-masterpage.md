---
ID: 1446
post_title: >
  Navigate content pages by using a top
  menu, a telerik radajaxpanel and
  response.redirect in the MasterPage
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/03/navigate-content-pages-by-using-a-top-menu-a-telerik-radajaxpanel-and-response-redirect-in-the-masterpage/
published: true
post_date: 2010-06-03 17:02:46
---
<p>When you use a MasterPage with a menu and navigate between you’re content pages in normal ASP .NET, you will see a brief flickering, caused by the ASP .NET postback. You can prevent this flickering by ajaxifying the postback.</p>  <p>This can be done by using the Telerik RadAjaxPanel. In my case I used LinkButtons in the masterpage for navigating the content pages and surrounded the Linbuttons by a Telerik RadAjaxPanel. The click events of the LinkButtons use Reponse.Redirect to navigate between the content pages.</p>  <p>&#160;</p>  <p><strong>Site.Master</strong></p>  <pre class="code"><span style="background: yellow">&lt;%</span><span style="color: blue">@ </span><span style="color: maroon">Master </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;Site.master.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;WebApplication1.SiteMaster&quot; </span><span style="background: yellow">%&gt;

&lt;%</span><span style="color: blue">@ </span><span style="color: maroon">Register </span><span style="color: red">Assembly</span><span style="color: blue">=&quot;Telerik.Web.UI&quot; </span><span style="color: red">Namespace</span><span style="color: blue">=&quot;Telerik.Web.UI&quot; </span><span style="color: red">TagPrefix</span><span style="color: blue">=&quot;telerik&quot; </span><span style="background: yellow">%&gt;
</span><span style="color: blue">&lt;!</span><span style="color: maroon">DOCTYPE </span><span style="color: red">html PUBLIC </span><span style="color: blue">&quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot; &quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;&gt;
&lt;</span><span style="color: maroon">html </span><span style="color: red">xmlns</span><span style="color: blue">=&quot;http://www.w3.org/1999/xhtml&quot;&gt;
&lt;</span><span style="color: maroon">head </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: maroon">title</span><span style="color: blue">&gt;</span>Test Page<span style="color: blue">&lt;/</span><span style="color: maroon">title</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">link </span><span style="color: red">href</span><span style="color: blue">=&quot;Styles/Master.css&quot; </span><span style="color: red">rel</span><span style="color: blue">=&quot;stylesheet&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot; /&gt;
    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">ContentPlaceHolder </span><span style="color: red">ID</span><span style="color: blue">=&quot;HeadContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">ContentPlaceHolder</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">head</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">body</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">form </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">class</span><span style="color: blue">=&quot;form&quot;&gt;
&lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadScriptManager </span><span style="color: red">ID</span><span style="color: blue">=&quot;generalRadScriptManager&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; /&gt;
</span><span style="color: #006400">&lt;!-- One RadAjaxManager for all content pages --&gt; 
</span><span style="color: blue">&lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadAjaxManager </span><span style="color: red">ID</span><span style="color: blue">=&quot;generalRadAjaxManager&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; /&gt;
</span><span style="color: #006400">&lt;!-- One RadAjaxLoadingPanel for all content pages --&gt; 
</span><span style="color: blue">&lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadAjaxLoadingPanel </span><span style="color: red">ID</span><span style="color: blue">=&quot;generalRadAjaxLoadingPanel&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">BackgroundPosition</span><span style="color: blue">=&quot;Center&quot; </span><span style="color: red">Skin</span><span style="color: blue">=&quot;Default&quot; /&gt;
&lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;page&quot;&gt;
    &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;inside&quot;&gt;
        &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;header&quot;&gt;
            </span><span style="color: #006400">&lt;!-- All postback's in the RadAjaxPanel1 will be converted to AJAX postback's and the page will not flicker on navigation --&gt;
            </span><span style="color: blue">&lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadAjaxPanel </span><span style="color: red">ID</span><span style="color: blue">=&quot;RadAjaxPanel1&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">LoadingPanelID</span><span style="color: blue">=&quot;generalRadAjaxLoadingPanel&quot;&gt;
                &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;navigation&quot;&gt;
                    &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;navigationPrimary&quot;&gt;
                        &lt;</span><span style="color: maroon">ul</span><span style="color: blue">&gt; 
                            &lt;</span><span style="color: maroon">li</span><span style="color: blue">&gt;&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton </span><span style="color: red">ID</span><span style="color: blue">=&quot;administrationLinkButton&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">onclick</span><span style="color: blue">=&quot;AdministrationLinkButton_Click&quot;&gt;</span>Menu1<span style="color: blue">&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton</span><span style="color: blue">&gt;&lt;/</span><span style="color: maroon">li</span><span style="color: blue">&gt;
                            &lt;</span><span style="color: maroon">li</span><span style="color: blue">&gt;&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton </span><span style="color: red">ID</span><span style="color: blue">=&quot;zakelijkLinkButton&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">onclick</span><span style="color: blue">=&quot;AdministrationLinkButton_Click&quot;&gt;Menu2</span><span style="color: blue">&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton</span><span style="color: blue">&gt;&lt;/</span><span style="color: maroon">li</span><span style="color: blue">&gt;
                        &lt;/</span><span style="color: maroon">ul</span><span style="color: blue">&gt;
                    &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;navigationSeparator&quot;&gt;&lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;navigationSecondairy&quot;&gt;
                        &lt;</span><span style="color: maroon">ul</span><span style="color: blue">&gt; 
                            &lt;</span><span style="color: maroon">li</span><span style="color: blue">&gt;&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton </span><span style="color: red">ID</span><span style="color: blue">=&quot;customerLinkButton&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">onclick</span><span style="color: blue">=&quot;CustomerLinkButton_Click&quot;&gt;SubMenu1</span><span style="color: blue">&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton</span><span style="color: blue">&gt;&lt;/</span><span style="color: maroon">li</span><span style="color: blue">&gt;
                            &lt;</span><span style="color: maroon">li</span><span style="color: blue">&gt;&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton </span><span style="color: red">ID</span><span style="color: blue">=&quot;PakkettenLinkButton&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">onclick</span><span style="color: blue">=&quot;AdministrationLinkButton_Click&quot;&gt;</span>SubMenu2<span style="color: blue">&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton</span><span style="color: blue">&gt;&lt;/</span><span style="color: maroon">li</span><span style="color: blue">&gt;
                            &lt;</span><span style="color: maroon">li</span><span style="color: blue">&gt;&lt;/</span><span style="color: maroon">li</span><span style="color: blue">&gt;
                        &lt;/</span><span style="color: maroon">ul</span><span style="color: blue">&gt;
                    &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
                &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadAjaxPanel</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
        &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;content&quot;&gt;
            &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">ContentPlaceHolder </span><span style="color: red">ID</span><span style="color: blue">=&quot;MainContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; /&gt;
        &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
        &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;footerPlaceholder&quot;&gt;&lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;footer&quot;&gt;
        &lt;</span><span style="color: maroon">ul </span><span style="color: red">class</span><span style="color: blue">=&quot;footerLeftNav&quot;&gt;
        &lt;</span><span style="color: maroon">li</span><span style="color: blue">&gt;</span>Test<span style="color: blue">&lt;/</span><span style="color: maroon">li</span><span style="color: blue">&gt;
        &lt;</span><span style="color: maroon">li</span><span style="color: blue">&gt;Test</span><span style="color: blue">&lt;/</span><span style="color: maroon">li</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: maroon">ul</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">form</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">body</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">html</span><span style="color: blue">&gt;

</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><strong>Site.Master.cs</strong></p>

<p>using System;
  <br />using System.Collections.Generic;

  <br />using System.Linq;

  <br />using System.Web;

  <br />using System.Web.UI;

  <br />using System.Web.UI.WebControls; </p>

<p>namespace WebApplication1
  <br />{

  <br />&#160;&#160;&#160; public partial class SiteMaster : System.Web.UI.MasterPage

  <br />&#160;&#160;&#160; {

  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; protected void Page_Load(object sender, EventArgs e)

  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; { </p>

<p>&#160;&#160;&#160;&#160;&#160;&#160;&#160; }
  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; protected void AdministrationLinkButton_Click(object sender, EventArgs e)

  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; {

  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; Response.Redirect(&quot;Default.aspx&quot;);

  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; }

  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; protected void CustomerLinkButton_Click(object sender, EventArgs e)

  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; {

  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; Response.Redirect(&quot;CustomerOverview.aspx&quot;);

  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; }

  <br />&#160;&#160;&#160; }

  <br />}</p>

<p>&#160;</p>

<p><strong>Master.css</strong></p>

<pre class="code"><span style="color: maroon">*
</span>{
    <span style="color: red">margin</span>: <span style="color: blue">0px</span>; <span style="color: #006400">/* All elements start with 0px margin */
    </span><span style="color: red">padding</span>: <span style="color: blue">0px</span>;  <span style="color: #006400">/* All elements start with 0px padding */
</span>}
<span style="color: maroon">html
</span>{
    <span style="color: red">height</span>: <span style="color: blue">100%</span>; <span style="color: #006400">/* Must be 100% for footer at the bottom of the page */
    </span><span style="color: red">font-family</span>: <span style="color: blue">Arial, Helvetica, sans-serif</span>;
    <span style="color: red">font-size</span>: <span style="color: blue">100%</span>;
    <span style="color: red">font-weight</span>: <span style="color: blue">normal</span>;
    <span style="color: red">color</span>: <span style="color: blue">#222</span>;
}
<span style="color: maroon">body
</span>{
    <span style="color: red">height</span>: <span style="color: blue">100%</span>; <span style="color: #006400">/* Must be 100% for footer at the bottom of the page */
</span>}
<span style="color: maroon">form
</span>{
    <span style="color: red">height</span>: <span style="color: blue">100%</span>; <span style="color: #006400">/* Must be 100% for footer at the bottom of the page */
</span>}
<span style="color: maroon">a
</span>{
    <span style="color: red">color</span>: <span style="color: blue">#222</span>;
    <span style="color: red">text-decoration</span>: <span style="color: blue">none</span>;
}
<span style="color: maroon">div.page
</span>{
    <span style="color: red">margin-right</span>: <span style="color: blue">auto</span>; <span style="color: #006400">/* Center the page */
    </span><span style="color: red">margin-left</span>:<span style="color: blue">auto</span>; <span style="color: #006400">/* Center the page */
    </span><span style="color: red">height</span>: <span style="color: blue">100%</span>;  <span style="color: #006400">/* Must be 100% for footer at the bottom of the page */
    </span><span style="color: red">text-align</span>: <span style="color: blue">left</span>;
    <span style="color: red">width</span>: <span style="color: blue">1000px</span>; <span style="color: #006400">/* Fixed width for screen resolution 1024px optimalisation */
</span>}
<span style="color: maroon">div.inside
</span>{
    <span style="color: red">border-left</span>: <span style="color: blue">1px solid rgb(224,225,226)</span>;
    <span style="color: red">border-right</span>: <span style="color: blue">1px solid rgb(224,225,226)</span>;
    <span style="color: red">min-height</span>: <span style="color: blue">100%</span>;  <span style="color: #006400">/* Must be 100% for footer at the bottom of the page, using min-height instead of height allows content to be larger then intial page size */
    </span><span style="color: red">margin-bottom</span>: <span style="color: blue">-33px</span>; <span style="color: #006400">/* Negative bottom margin is used for correct the 100% height with the height of the footer, else vertical scrollbars will be shown */
</span>}
<span style="color: maroon">div.header
</span>{
    <span style="color: red">padding</span>: <span style="color: blue">10px 0px 8px 0px</span>;
}
<span style="color: maroon">div.header img
</span>{
    <span style="color: red">height</span>: <span style="color: blue">60px</span>;
    <span style="color: red">margin-left</span>: <span style="color: blue">20px</span>;
    <span style="color: red">width</span>: <span style="color: blue">194px</span>;
}
<span style="color: maroon">div.content
</span>{
    <span style="color: red">color</span>: <span style="color: blue">#666</span>;
    <span style="color: red">font-size</span>: <span style="color: blue">70%</span>;
    <span style="color: red">padding</span>: <span style="color: blue">10px 15px 15px 15px</span>;
}
<span style="color: maroon">div.navigation
</span>{
    <span style="color: red">border-bottom</span>: <span style="color: blue">2px solid rgb(255,102,0)</span>;
    <span style="color: red">position</span>: <span style="color: blue">absolute</span>;
    <span style="color: red">top</span>: <span style="color: blue">0px</span>;
    <span style="color: red">width</span>: <span style="color: blue">998px</span>;
}
<span style="color: maroon">div.navigationSeparator
</span>{
    <span style="color: red">border-top</span>: <span style="color: blue">1px solid rgb(222,222,222)</span>;
    <span style="color: red">margin-left</span>: <span style="color: blue">279px</span>;
}
<span style="color: maroon">div.navigationPrimary ul
</span>{
    <span style="color: red">height</span>: <span style="color: blue">26px</span>;
    <span style="color: red">margin-top</span>: <span style="color: blue">13px</span>;
    <span style="color: red">padding-left</span>: <span style="color: blue">299px</span>;
}
<span style="color: maroon">div.navigationPrimary ul li
</span>{
    <span style="color: red">background</span>: <span style="color: blue">url(../Images/TabLeft.gif) no-repeat scroll left top</span>;
    <span style="color: red">float</span>: <span style="color: blue">left</span>; <span style="color: #006400">/* Makes the unoderdered list flow horizontal instead of vertical */
    </span><span style="color: red">font-weight</span>: <span style="color: blue">bold</span>;
    <span style="color: red">font-size</span>: <span style="color: blue">75%</span>;
    <span style="color: red">height</span>: <span style="color: blue">26px</span>;
    <span style="color: red">line-height</span>: <span style="color: blue">26px</span>;
    <span style="color: red">list-style-type</span>: <span style="color: blue">none</span>; <span style="color: #006400">/* Don't display bullets */
    </span><span style="color: red">margin</span>: <span style="color: blue">0px 4px 0px 0px</span>;
    <span style="color: red">text-decoration</span>: <span style="color: blue">none</span>;
    <span style="color: red">text-transform</span>: <span style="color: blue">uppercase</span>;
    <span style="color: red">white-space</span>: <span style="color: blue">nowrap</span>;
}
<span style="color: maroon">div.navigationPrimary ul li a
</span>{
    <span style="color: red">background</span>: <span style="color: blue">url(../Images/TabRight.gif) no-repeat scroll right top</span>;
    <span style="color: red">float</span>: <span style="color: blue">left</span>;
    <span style="color: red">height</span>: <span style="color: blue">26px</span>;
    <span style="color: red">line-height</span>: <span style="color: blue">26px</span>;
    <span style="color: red">padding</span>: <span style="color: blue">0px 15px 0px 15px</span>;
}
<span style="color: maroon">div.navigationPrimary ul li a:hover
</span>{
    <span style="color: red">color</span>: <span style="color: blue">rgb(255,102,0)</span>;
}
<span style="color: maroon">div.navigationSecondairy ul
</span>{
    <span style="color: red">padding-left</span>: <span style="color: blue">310px</span>;
}
<span style="color: maroon">div.navigationSecondairy ul li
</span>{
    <span style="color: red">background</span>: <span style="color: blue">url(../Images/MenuSeparator.gif) no-repeat scroll left 18px</span>;
    <span style="color: red">float</span>: <span style="color: blue">left</span>; <span style="color: #006400">/* Makes the unoderdered list flow horizontal instead of vertical */
    </span><span style="color: red">font-size</span>: <span style="color: blue">80%</span>;
    <span style="color: red">height</span>: <span style="color: blue">30px</span>;
    <span style="color: red">list-style-type</span>: <span style="color: blue">none</span>; <span style="color: #006400">/* Don't display bullets */
    </span><span style="color: red">margin-right</span>: <span style="color: blue">12px</span>;
    <span style="color: red">padding-top</span>: <span style="color: blue">12px</span>;
    <span style="color: red">padding-left</span>: <span style="color: blue">10px</span>;
    <span style="color: red">white-space</span>: <span style="color: blue">nowrap</span>;
}
<span style="color: maroon">div.navigationSecondairy ul li a
</span>{
    <span style="color: red">float</span>: <span style="color: blue">left</span>;
}
<span style="color: maroon">div.navigationSecondairy ul li a:hover
</span>{
    <span style="color: red">color</span>: <span style="color: blue">rgb(255,102,0)</span>;
}
<span style="color: maroon">div.footerPlaceholder
</span>{
    <span style="color: red">height</span>: <span style="color: blue">33px</span>; <span style="color: #006400">/* The height should be equal to the full height of the footer (including any padding or borders you may add). Without the &quot;footerPlaceholder&quot; div, the content will flow beneath the footer */
</span>}
<span style="color: maroon">div.footer
</span>{
    <span style="color: red">background</span>: <span style="color: blue">url(../Images/Footer.gif) #f60 repeat-x</span>;
    <span style="color: red">color</span>: <span style="color: blue">rgb(255,255,255)</span>;
    <span style="color: red">font-size</span>: <span style="color: blue">60%</span>;
    <span style="color: red">padding</span>: <span style="color: blue">10px 46px 10px 46px</span>;
    <span style="color: red">width</span>: <span style="color: blue">906px</span>;
}
<span style="color: maroon">ul.footerLeftNav
</span>{
    <span style="color: red">margin</span>: <span style="color: blue">0px</span>;
    <span style="color: red">padding</span>: <span style="color: blue">0px</span>;
    <span style="color: red">page-break-inside</span>: <span style="color: blue">avoid</span>;
    <span style="color: red">list-style-position</span>: <span style="color: blue">outside</span>;
    <span style="color: red">list-style-type</span>: <span style="color: blue">none</span>;
}
<span style="color: maroon">ul.footerLeftNav li
</span>{
    <span style="color: red">display</span>: <span style="color: blue">inline</span>;
    <span style="color: red">padding-right</span>: <span style="color: blue">18px</span>;
}</pre>
<a href="http://11011.net/software/vspaste"></a>