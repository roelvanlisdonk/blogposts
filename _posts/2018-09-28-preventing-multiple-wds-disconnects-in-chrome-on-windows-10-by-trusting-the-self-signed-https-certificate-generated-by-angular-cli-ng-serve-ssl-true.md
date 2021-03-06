---
ID: 5248
post_title: 'Preventing multiple WDS disconnects in Chrome on Windows 10, by trusting the self-signed https certificate, generated by Angular CLI ng serve &#8211;ssl true'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/09/28/preventing-multiple-wds-disconnects-in-chrome-on-windows-10-by-trusting-the-self-signed-https-certificate-generated-by-angular-cli-ng-serve-ssl-true/
published: true
post_date: 2018-09-28 16:49:39
---
<p>
 </p><p>If you use ng serve with the parameter –ssl true, to serve your Angular application. 
</p><p>It will generate a self-signed https certificate, so you can run the Angular application on localhost using HTTPS.
</p><p>By default this certificate is NOT trusted by your browser, so you will get a red cross, left to the url.
</p><p>Because this certificate is not trusted, you might get multiple WDS disconnect errors in the chrome developer tools console.
</p><p>Sometimes ending in a never-ending loop.
</p><p>If you want to trust the self-signed https certificate:
</p><ul><li>click on the red cross (a popup opens)
</li><li>choose Certificate
</li><li>Click on Details
</li><li>Click on Copy to file
</li></ul><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/09/092818_1449_Preventingm1.png" alt=""/>
	</p><p>
 </p><p>Press next
</p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/09/092818_1449_Preventingm2.png" alt=""/>
	</p><p>
 </p><p>Choose DER encoded binary X.509 (.CER)
</p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/09/092818_1449_Preventingm3.png" alt=""/>
	</p><p>Enter C:\Temp\localhost.cer
</p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/09/092818_1449_Preventingm4.png" alt=""/>
	</p><p>
 </p><p>Press Finish
</p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/09/092818_1449_Preventingm5.png" alt=""/>
	</p><p>
 </p><p>Go to C:\Temp with the explorer and double click on the localhost.cer file.
</p><p>
 </p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/09/092818_1449_Preventingm6.png" alt=""/>
	</p><p>
 </p><p>Press Install Certificate…
</p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/09/092818_1449_Preventingm7.png" alt=""/>
	</p><p>
 </p><p>Choose "Local Machine" if you want the certificate be trusted for all user of this computer.
</p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/09/092818_1449_Preventingm8.png" alt=""/>
	</p><p>
 </p><p>
 </p><p><strong>To remove the certificate on Windows 10
</strong></p><ul><li>Open Start, type <span style="color:#222222; font-family:Arial; background-color:white">certmgr.msc</span>
		</li><li>Click on "Trusted Root Certification Authorities" &gt; Certificates
</li><li>Right click on localhost and choose Delete
</li></ul><p>
 </p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/09/092818_1449_Preventingm9.png" alt=""/></p>