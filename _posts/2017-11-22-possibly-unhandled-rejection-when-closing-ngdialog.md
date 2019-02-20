---
ID: 5139
post_title: '&#8220;Possibly unhandled rejection&#8221; when closing ngDialog'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/11/22/possibly-unhandled-rejection-when-closing-ngdialog/
published: true
post_date: 2017-11-22 21:15:11
---
<p> 
 </p><p><span style="font-family:Times New Roman; font-size:12pt">Found my solution at: https://github.com/angular/material/issues/10369 
</span></p><p><span style="font-family:Times New Roman; font-size:12pt">When using the openConfirm function use: 
</span></p><p><span style="font-family:Times New Roman; font-size:12pt">TypeScript: 
</span></p><p><span style="font-family:Courier New"><span style="color:black; font-size:9pt">ngDialog </span><span style="font-size:12pt">
			</span></span></p><p><span style="font-family:Courier New"><span style="color:black; font-size:9pt">.openConfirm(dialogOptions) </span><span style="font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New"><span style="font-size:9pt">.catch(<span style="color:blue">function<span style="color:black"> dialogCloseErrorCallback(reason: <span style="color:blue">any<span style="color:black">) { </span></span></span></span></span><span style="font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New"><span style="font-size:9pt">        <span style="color:green">// ngDialog v1.4.0 throws an exception, when closing the dialog with reason "undefined". </span></span><span style="font-size:12pt">
			</span></span></p><p><span style="font-family:Courier New"><span style="color:green; font-size:9pt">        // Prevent this error: </span><span style="font-size:12pt">
			</span></span></p><p><span style="color:blue; font-family:Courier New"><span style="font-size:9pt">    if<span style="color:black"> (reason !== undefined) { </span></span><span style="font-size:12pt">
			</span></span></p><p><span style="color:blue; font-family:Courier New"><span style="font-size:9pt">        throw<span style="color:black">
					<span style="color:blue">new<span style="color:black"> Error(<span style="color:#a31515">`Error when closing the dialog: [<span style="color:blue">${<span style="color:black">reason<span style="color:blue">}<span style="color:#a31515">].`<span style="color:black">); </span></span></span></span></span></span></span></span></span></span><span style="font-size:12pt">
			</span></span></p><p><span style="font-family:Courier New"><span style="color:black; font-size:9pt">    } </span><span style="font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">});
</span></p><p>
 </p><p><span style="font-family:Times New Roman; font-size:12pt">When using open, use:
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> openResult = self.ngDialog.open(dialogOptions);
</span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">if<span style="color:black"> (openResult.closePromise) {
</span></span></p><p><span style="color:black; font-family:Courier New"><span style="font-size:9pt">    openResult.closePromise</span><span style="font-size:9pt">.catch(<span style="color:blue">function<span style="color:black"> dialogCloseErrorCallback(reason: <span style="color:blue">any<span style="color:black">) { </span></span></span></span></span><span style="font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New"><span style="font-size:9pt">            <span style="color:green">// ngDialog v1.4.0 throws an exception, when closing the dialog with reason "undefined". </span></span><span style="font-size:12pt">
			</span></span></p><p><span style="font-family:Courier New"><span style="color:green; font-size:9pt">           // Prevent this error: </span><span style="font-size:12pt">
			</span></span></p><p><span style="color:blue; font-family:Courier New"><span style="font-size:9pt">        if<span style="color:black"> (reason !== undefined) { </span></span><span style="font-size:12pt">
			</span></span></p><p><span style="color:blue; font-family:Courier New"><span style="font-size:9pt">            throw<span style="color:black">
					<span style="color:blue">new<span style="color:black"> Error(<span style="color:#a31515">`Error when closing the dialog: [<span style="color:blue">${<span style="color:black">reason<span style="color:blue">}<span style="color:#a31515">].`<span style="color:black">); </span></span></span></span></span></span></span></span></span></span><span style="font-size:12pt">
			</span></span></p><p><span style="font-family:Courier New"><span style="color:black; font-size:9pt">        } </span><span style="font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    });
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">}</span></p>