---
ID: 5117
post_title: 'Uncaught SyntaxError: Unexpected token in JSON at position 30 with escaped unicode character'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/09/12/uncaught-syntaxerror-unexpected-token-in-json-at-position-30-with-escaped-unicode-character/
published: true
post_date: 2017-09-12 15:55:10
---
<p>
 </p><p><span style="color:#555555; font-family:Arial; font-size:12pt">When you execute the JavaScript code:
</span></p><p><span style="color:#555555; font-family:Courier New; font-size:10pt">JSON.parse("\"This is a unicode character: \u0007\"")
</span></p><p><span style="color:#555555; font-family:Arial; font-size:12pt">in a browser you will get the error:
</span></p><p><span style="color:#555555; font-family:Arial; font-size:12pt">Uncaught SyntaxError: Unexpected token in JSON at position 30<br/>     at JSON.parse (&lt;anonymous&gt;)<br/>     at &lt;anonymous&gt;:1:6
</span></p><p><span style="color:#555555; font-family:Arial; font-size:12pt">I fixed this by altering the C# code that returned the JSON.
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">public<span style="color:black">
					<span style="color:blue">static<span style="color:black">
							<span style="color:blue">class<span style="color:black">
									<span style="color:#2b91af">MvcHelper<span style="color:black">
										</span></span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">    {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">public<span style="color:black">
					<span style="color:blue">static<span style="color:black">
							<span style="color:#2b91af">ActionResult<span style="color:black"> ConvertToJsonActionResult(<span style="color:blue">object<span style="color:black"> data)
</span></span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">var<span style="color:black"> content = ConvertToCamelCaseJsonString(data);
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">            content = RemoveEscapedUnicodeCharactersFromString(content);
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">return<span style="color:black"> ConvertStringToJsonContentResult(content);
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        }
</span></p><p>
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">private<span style="color:black">
					<span style="color:blue">static<span style="color:black">
							<span style="color:blue">string<span style="color:black"> ConvertToCamelCaseJsonString(<span style="color:blue">object<span style="color:black"> data)
</span></span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">var<span style="color:black"> serializationSettings =
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">new<span style="color:black">
					<span style="color:#2b91af">JsonSerializerSettings<span style="color:black">
						</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    ContractResolver = <span style="color:blue">new<span style="color:black">
					<span style="color:#2b91af">CamelCasePropertyNamesContractResolver<span style="color:black">()
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                };
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">return<span style="color:black">
					<span style="color:#2b91af">JsonConvert<span style="color:black">.SerializeObject(data, serializationSettings);
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        }
</span></p><p>
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">private<span style="color:black">
					<span style="color:blue">static<span style="color:black">
							<span style="color:#2b91af">ContentResult<span style="color:black"> ConvertStringToJsonContentResult(<span style="color:blue">string<span style="color:black"> content)
</span></span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">return<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">new<span style="color:black">
					<span style="color:#2b91af">ContentResult<span style="color:black">()
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    Content = content,
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    ContentType = <span style="color:#a31515">"application/json"<span style="color:black">,
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    ContentEncoding = System.Text.<span style="color:#2b91af">Encoding<span style="color:black">.UTF8
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                };
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        }
</span></p><p>
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">private<span style="color:black">
					<span style="color:blue">static<span style="color:black">
							<span style="color:blue">string<span style="color:black"> RemoveEscapedUnicodeCharactersFromString(<span style="color:blue">string<span style="color:black"> content)
</span></span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">var<span style="color:black"> regex = <span style="color:blue">new<span style="color:black"> System.Text.RegularExpressions.<span style="color:#2b91af">Regex<span style="color:black">(<span style="color:maroon">@"\\+[uU]([0-9A-Fa-f]{4})"<span style="color:black">);
</span></span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">return<span style="color:black"> regex.Replace(content, <span style="color:blue">string<span style="color:black">.Empty);
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        }
</span></p><p><span style="color:black"><span style="font-family:Consolas; font-size:9pt">    }</span><span style="color:#555555; font-family:Arial; font-size:12pt">
			</span></span></p><p>
 </p><p><span style="color:#555555; font-family:Arial; font-size:12pt">Then you can convert your C# ViewModel to a Json ActionResult:
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        [<span style="color:#2b91af">HttpPost<span style="color:black">]
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">public<span style="color:black">
					<span style="color:#2b91af">ActionResult<span style="color:black"> WizardData(<span style="color:blue">int<span style="color:black"> taakId)
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">var<span style="color:black"> model = <span style="color:blue">new<span style="color:black">
							<span style="color:#2b91af">MyViewModelViewModel<span style="color:black">();
</span></span></span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">return<span style="color:black">
					<span style="color:#2b91af">MvcHelper<span style="color:black">.ConvertToJsonActionResult(model);
</span></span></span></span></span></p><p><span style="color:black"><span style="font-family:Consolas; font-size:9pt">        }</span><span style="color:#555555; font-family:Arial; font-size:12pt">
			</span></span></p><p>
 </p><p>
 </p><p>
 </p><p>
 </p><p>
 </p><p>
 </p><p>
 </p><p>
 </p>