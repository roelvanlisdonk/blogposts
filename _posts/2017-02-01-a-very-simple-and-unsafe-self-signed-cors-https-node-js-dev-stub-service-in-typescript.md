---
ID: 5059
post_title: >
  A very simple and unsafe :-),
  self-signed, CORS https node.js dev stub
  service in TypeScript
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/02/01/a-very-simple-and-unsafe-self-signed-cors-https-node-js-dev-stub-service-in-typescript/
published: true
post_date: 2017-02-01 22:08:12
---
<pre><p><br /></p><p>
<font size="1">const https = require(&quot;https&quot;);
const fs = require(&quot;fs&quot;);

// To create the key.pem and cert.pem files for dev, use opensll:
// openssl req -newkey rsa:2048 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem
//
// Cert and key are created for hosheader &quot;stub.service.am.dev&quot;.
// Make sure the hosts file on windows contains:
// 127.0.0.1	stub.service.am.dev
const options = {
    key: fs.readFileSync(&quot;./key.pem&quot;),
    cert: fs.readFileSync(&quot;./cert.pem&quot;)
};
const port = 4433;

https.createServer(options, function (req: any, res: any) {
    // Allow calls from all domains, for all methods ans request headers.
    res.setHeader(&quot;Access-Control-Allow-Origin&quot;, &quot;*&quot;);
    res.setHeader(&quot;Access-Control-Allow-Credentials&quot;, true);
    res.setHeader(&quot;Access-Control-Allow-Methods&quot;, &quot;*&quot;);
    res.setHeader(&quot;Access-Control-Allow-Headers&quot;, &quot;*&quot;);

    res.end(`Request received on server. Path Hit: ${res.url}`);
}).listen(port, function() {
    console.log(`Stub service listing on ${port}`);
});
</font></p><p><font size="1"><br /></font></p><p><font size="1">Just enter </font><a href="https://stub.service.am.dev:4433"><font size="1">https://stub.service.am.dev:4433</font></a><font size="1"> and it should respond with:</font></p><pre>Request received on server. Path Hit: undefined</pre><p>
</p><p>
</p></pre>