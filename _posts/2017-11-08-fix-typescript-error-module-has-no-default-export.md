---
ID: 5132
post_title: 'Fix: TypeScript error Module &#8216;&#8230;&#8217; has no default export'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/11/08/fix-typescript-error-module-has-no-default-export/
published: true
post_date: 2017-11-08 07:49:28
---
<p>
 </p><p>When I compiled my TypeScript project I got the error: [ts] Module '"c:/dev/am/common/element/after-visible"' has not default export:
</p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2017/11/110817_0649_FixTypeScri1.png" alt=""/>
	</p><p>
 </p><p>This was caused by the fact, that I forgot to surround "afterVisible" with "{ }".
</p><p>The contents of the after-visible.ts module was:
</p><p>
 </p><p style="background: white"><span style="color:green; font-family:Consolas; font-size:10pt">/**<span style="color:black">
			</span></span></p><p style="background: white"><span style="color:green; font-family:Consolas; font-size:10pt"> * Check the DOM repeatedly to see if the given element is visible, when element is visible call given function.<span style="color:black">
			</span></span></p><p style="background: white"><span style="color:green; font-family:Consolas; font-size:10pt"> */<span style="color:black">
			</span></span></p><p style="background: white"><span style="color:blue; font-family:Consolas; font-size:10pt">export<span style="color:black">
				<span style="color:blue">function<span style="color:black"> afterVisible(selector: string, fn: (element?: HTMLElement) <span style="color:blue">=&gt;<span style="color:black"> void, interval: number = <span style="color:#09885a">10<span style="color:black">, retryCount: number = <span style="color:#09885a">30<span style="color:black">): void {
</span></span></span></span></span></span></span></span></span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">
			<span style="color:blue">const<span style="color:black"> element = &lt;HTMLElement&gt;document.querySelector(selector);
</span></span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">
			<span style="color:blue">if<span style="color:black"> (element) {
</span></span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">
			<span style="color:blue">const<span style="color:black"> elementIsVisible = element.offsetWidth &gt; <span style="color:#09885a">0<span style="color:black"> &amp;&amp; element.offsetHeight &gt; <span style="color:#09885a">0<span style="color:black">;
</span></span></span></span></span></span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">
			<span style="color:blue">if<span style="color:black"> (elementIsVisible) {
</span></span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">            fn(element);
</span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">
			<span style="color:blue">return<span style="color:black">;
</span></span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">        }
</span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">    }
</span></p><p style="background: white">    
 </p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">    setTimeout(<span style="color:blue">function<span style="color:black"> afterVisibleSetTimeoutElapsed() {
</span></span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">
			<span style="color:blue">if<span style="color:black"> (retryCount === <span style="color:#09885a">0<span style="color:black">) {
</span></span></span></span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">
			<span style="color:blue">if<span style="color:black"> (console) {
</span></span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">                console.log(<span style="color:#a31515">`Element '<span style="color:blue">${<span style="color:black">selector<span style="color:blue">}<span style="color:#a31515">' does not exist or was not visible.`<span style="color:black">);
</span></span></span></span></span></span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">            }
</span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">        } <span style="color:blue">else<span style="color:black"> {
</span></span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">
			<span style="color:green">// Try again<span style="color:black">
				</span></span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">            afterVisible(selector, fn, retryCount - <span style="color:#09885a">1<span style="color:black">, interval);
</span></span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">        }
</span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">    }, interval);
</span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">}
</span></p><p>
 </p><p>
 </p><p>So when you want to use the function afterVisible in an other function you will have to import it like so:
</p><p>
 </p><p style="background: white"><span style="color:blue; font-family:Consolas; font-size:10pt">import<span style="color:black"> { afterVisible } <span style="color:blue">from<span style="color:black">
						<span style="color:#a31515">"./after-visible"<span style="color:black">;
</span></span></span></span></span></span></p><p style="background: white">
 </p><p style="background: white"><span style="color:blue; font-family:Consolas; font-size:10pt">function<span style="color:black"> focus(element: HTMLElement) {
</span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">    element.focus();
</span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">}
</span></p><p style="background: white">
 </p><p style="background: white"><span style="color:green; font-family:Consolas; font-size:10pt">/**<span style="color:black">
			</span></span></p><p style="background: white"><span style="color:green; font-family:Consolas; font-size:10pt"> * Check the DOM repeatedly to see if the given element is visible, when element is visible focus it.<span style="color:black">
			</span></span></p><p style="background: white"><span style="color:green; font-family:Consolas; font-size:10pt"> */<span style="color:black">
			</span></span></p><p style="background: white"><span style="color:blue; font-family:Consolas; font-size:10pt">export<span style="color:black">
				<span style="color:blue">function<span style="color:black"> focusAfterVisible(selector: string, interval: number = <span style="color:#09885a">10<span style="color:black">, retryCount: number = <span style="color:#09885a">30<span style="color:black">): void {
</span></span></span></span></span></span></span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">    afterVisible(selector, focus, interval, retryCount);
</span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">}
</span></p><p>
 </p><p>
 </p><p>
 </p><p>
 </p><p>
 </p>