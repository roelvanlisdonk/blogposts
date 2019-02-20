---
ID: 4634
post_title: Some DEVintersection notes (in dutch)
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/10/15/some-devintersection-notes-in-dutch/
published: true
post_date: 2015-10-15 22:29:04
---
<p>&#160;</p>  <p><strong>OpenSource en crossplatform</strong></p>  <p>Is de toekomst, maar waarom krijg je dat van Microsoft en partners te horen? Daar is 1 reden voor bij Microsoft:</p>  <p><font color="#0000ff" size="4">We want your FOR loop!!!</font></p>  <p>Wij (microsoft) verkopen compute, wij willen jouw code draaien, windows is afgeschreven als cach cow.</p>  <p>&#160;</p>  <p><strong>Windows containers</strong></p>  <p>Kan zeer goed gebruikt worden voor <strong><font color="#666666">immutable infrastructure</font></strong></p>  <p>&#160;</p>  <p><strong>Virtualisatie</strong></p>  <ul>   <li>Virtual Machines (opstarten in minuten, grote: zo groot als de software die je erin zet + volledige operating system)</li>    <li>Containers (opstarten in seconden, grote: zo groot als de software die je erin zet)</li>    <li>Virtual processen, zoals in GO, Erlang / Elixer ( in 1 ms opgestart, grote: +/- 4kb) = performance niet normaal :-)</li> </ul>  <p>&#160;</p>  <p><strong>User Experience</strong></p>  <p><a href="http://chulakov.com/menu">http://chulakov.com/menu</a></p>  <p><strong></strong></p>  <p><strong>JavaScript - Fetch API</strong></p>  <p>De opvolger van XMLHttpRequest,</p>  <p><a href="https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API">https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API</a></p>  <p>The Fetch API provides an interface for fetching resources (e.g., across the network.) It will seem familiar to anyone who has used XMLHttpRequest, but the new API provides a more powerful and flexible feature set.</p>  <p>&#160;</p>  <p><strong>HTTP2</strong></p>  <ul>   <li>geen bundeling meer nodig</li>    <li>geen image spriting meer nodig</li>    <li>Standaard TLS</li>    <li>Perfomance verbetering die behoorlijk kan oplopen van 50% tot 400%, zie <a href="https://http2.akamai.com/demo">https://http2.akamai.com/demo</a></li>    <li>Server push</li>    <li>Er wordt nog maar 1 verbinding gelegd en behouden, waarover gecommuniceerd wordt via onder andere multiplexing, frames hebben een ID.</li>    <li>Prioriteit geven aan bepaalde data in bepaalde situaties</li>    <li>Voor IIS beschikbaar in windows 10 / server 2016</li> </ul>  <p>&#160;</p>  <p><strong>ES6</strong></p>  <ul>   <li>Iterators</li>    <li>Generators</li>    <li>Template strings, let op je kunt waardes een stukjes tekst indexed, benaderen als je functie gebruikt bijv.: let items = test `${user.firstName} ${user.lastName}` let op de functie &quot;test&quot; wordt dan dus zonder haken aangeroepen, de test functies kan dan een values parameter hebben, waar de twee waardes in staan, lees meer op MDN.</li>    <li>Destruction</li>    <li>Symbol (kan gebruikt worden voor private members).</li>    <li>Lamda (=&gt;) heeft lexical scope, this je kunt altijd this. Gebruiken, zonder let self = this; of function.bind the gebruiken.</li>    <li>… = rest parameter, maar kan ook spread operator zijn, ligt eraan waar hij staat</li>    <li>Defaults voor parameters</li>    <li>Gebruik for(item of items) als vervanger van for(var i = 1; length; i &lt; length; i+=1) { }, indien index niet van belang is.</li> </ul>  <p><strong>JavaScript libraries die tegenwoordig gebruikt worden rondom modules:</strong></p>  <ul>   <li>Babel.js</li>    <li>Core.js</li>    <li>TypeScript</li>    <li>JSPM</li>    <li>System.js (kan conditional lazy, modules laden)</li>    <li>Webpack</li>    <li>Browserify</li>    <li>Bower</li>    <li>NPM</li> </ul>  <p>Allemaal hebben ze wat overlap, maar doen ze allemaal net wat anders.</p>  <p>&#160;</p>  <p><strong>Transpilers</strong></p>  <ul>   <li>TypeScript (gebruiken als je typesafety belangrijk vindt, anders babel.js gebruiken)</li>    <li>Babel.js</li>    <li>Traceur (niet gebruiken)</li> </ul>  <p><strong>Outsourcing</strong></p>  <ul>   <li>Naar lage loonlanden, is in vele gevallen, vele male duurder, dan zelf bouw of outsourcing in eigen land.</li> </ul>  <p>&#160;</p>  <p><strong>Scaffolding tool</strong></p>  <p><a href="http://yeoman.io/">http://yeoman.io/</a> het is krachtig om code / projecten te genereren, volgens mij gaat microsoft zelf hier ook gebruik van maken in Visual Studio.</p>  <p>&#160;</p>  <p><strong>Handige sites</strong></p>  <p><a href="http://caniuse.com/">http://caniuse.com/</a></p>  <p>ASP.NET 5 op ASP .NET Core (DNX) is de toekomst voor wat betreft ASP .NET</p>  <p>&#160;</p>  <p><strong>Uitzoeklijst</strong></p>  <p>En dan zijn er nog tal van zaken die op mijn uitzoeklijst zijn terecht gekomen:</p>  <ul>   <li>ASP .NET Kestrel</li>    <li><a href="https://www.nginx.com/">https://www.nginx.com/</a></li>    <li><a href="https://servicestack.net/features">https://servicestack.net/features</a>: “Thoughtfully architected, obscenely fast, thoroughly enjoyable web services for all”, A fast unified and integrated replacement for WCF, WebAPI en MVC</li>    <li>Een zoekmachine speciaal om dokters te vinden: <a href="http://www.healthgrades.com/">http://www.healthgrades.com/</a></li>    <li>En nog veel meer :-)</li> </ul>