---
ID: 5167
post_title: 'How to create WordPress blog posts from C# with HttpClient and the WordPress REST API on Docker for Windows 10'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/06/18/how-to-create-wordpress-blog-posts-from-c-with-httpclient-and-the-wordpress-rest-api-on-docker-for-windows-10/
published: true
post_date: 2018-06-18 11:20:51
---
<p> 
 </p><p><span style="font-family:Times New Roman; font-size:12pt">To create WordPress blog posts from C# I will be using docker container on my Windows 10 Pro installation. 
</span></p><p><span style="font-family:Times New Roman; font-size:12pt">Before installing docker on Windows 10 make sure the Windows 10 feature "Hyper-V" is enabled: 
</span></p><p> 
 </p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/06/061818_1210_Howtocreate1.png" alt=""/><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p> 
 </p><h1>Install docker on Windows 10 
</h1><p><span style="font-family:Times New Roman; font-size:12pt">I followed this blog post to install docker on Windows 10 
</span></p><p><span style="font-family:Times New Roman; font-size:12pt">https://docs.docker.com/docker-for-windows/install/#about-windows-containers 
</span></p><p> 
 </p><h1>Create WordPress docker container 
</h1><p><span style="font-family:Times New Roman; font-size:12pt">To create a WordPress docker container I followed this post: 
</span></p><p><span style="font-family:Times New Roman; font-size:12pt">https://docs.docker.com/compose/wordpress/ 
</span></p><p> 
 </p><h1>How to read blog post information from C# 
</h1><p><span style="font-family:Times New Roman; font-size:12pt">When the WordPress docker container is running, you should create your first blog post manually on http://localhost:8000. 
</span></p><p><span style="font-family:Times New Roman; font-size:12pt">Now reading all blog post data, is easy, because we can use an GET request without authentication, by using the C# code below.
</span></p><p>
 </p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/06/061918_0742_Howtocreate1.png" alt=""/><span style="font-family:Times New Roman; font-size:12pt"> 
</span></p><p>
 </p><h1>Installing JWT Authentication for WP-API plugin 
</h1><p><span style="font-family:Times New Roman; font-size:12pt">Now when you want to create a blog post from C# you will need to use a POST request with authentication. 
</span></p><p><span style="font-family:Times New Roman; font-size:12pt">I used JWT (JSON Web Tokens). 
</span></p><p><span style="font-family:Times New Roman; font-size:12pt">When you want to use JWT in WordPress you should first install the </span><span style="color:black; font-family:Segoe UI; font-size:10pt"><strong>JWT Authentication for WP-API</strong> plugin. </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="font-family:Times New Roman; font-size:12pt">After installing the plugin we must first edit two files before activating the plugin. 
</span></p><p> 
 </p><p> 
 </p><h3>Edit .htaccess file on Windows 
</h3><p> 
 </p><p><span style="font-family:Times New Roman; font-size:12pt">Get WordPress container name on windows: 
</span></p><ul><li>Open PowerShell and enter: 
</li><li><span style="color:#c00000">docker ps --all</span>
		</li></ul><p><span style="font-family:Times New Roman; font-size:12pt">Copy .htaccess file from docker container to local Windows host: 
</span></p><ul style="margin-left: 54pt"><li><span style="color:#c00000">docker cp wordpress_wordpress_1:/var/www/html/.htaccess .htaccess</span>
		</li></ul><p><span style="font-family:Times New Roman; font-size:12pt">Edit the file with your preferred editor (I used Visual Studio Code), add the rows in red: 
</span></p><p> 
 </p><p><span style="font-family:Courier New; font-size:8pt"># BEGIN WordPress 
</span></p><p><span style="font-family:Courier New; font-size:8pt">&lt;IfModule mod_rewrite.c&gt; 
</span></p><p><span style="font-family:Courier New; font-size:8pt">RewriteEngine On 
</span></p><p><span style="font-family:Courier New; font-size:8pt">RewriteBase / 
</span></p><p><span style="font-family:Courier New; font-size:8pt">RewriteRule ^index\.php$ - [L] 
</span></p><p><span style="font-family:Courier New; font-size:8pt">RewriteCond %{REQUEST_FILENAME} !-f 
</span></p><p><span style="font-family:Courier New; font-size:8pt">RewriteCond %{REQUEST_FILENAME} !-d 
</span></p><p><span style="font-family:Courier New; font-size:8pt">RewriteRule . /index.php [L] 
</span></p><p><span style="font-family:Courier New; font-size:8pt"><span style="color:red">RewriteCond %{HTTP:Authorization} ^(.*) </span>
		</span></p><p><span style="font-family:Courier New; font-size:8pt"><span style="color:red">RewriteRule ^(.*) - [E=HTTP_AUTHORIZATION:%1] </span>
		</span></p><p><span style="font-family:Courier New; font-size:8pt">&lt;/IfModule&gt; 
</span></p><p><span style="font-family:Courier New; font-size:8pt">SetEnvIf Authorization "(.*)" HTTP_AUTHORIZATION=$1 
</span></p><p><span style="font-family:Courier New; font-size:8pt"># END WordPress 
</span></p><p> 
 </p><p> 
 </p><p><span style="font-family:Times New Roman; font-size:12pt">Copy .htaccess file from local Windows host to Docker container: 
</span></p><ul style="margin-left: 54pt"><li><span style="color:#c00000">docker cp .htaccess wordpress_wordpress_1:/var/www/html/.htaccess </span>
		</li></ul><p> 
 </p><p> 
 </p><h3>Edit wp-config.php on Windows 
</h3><p> 
 </p><p><span style="font-family:Times New Roman; font-size:12pt">Get WordPress container name on windows: 
</span></p><ul><li>Open PowerShell and enter: 
</li><li><span style="color:#c00000">docker ps --all</span>
		</li></ul><p><span style="font-family:Times New Roman; font-size:12pt">Copy wp-config.php file from docker container to local Windows host: 
</span></p><ul style="margin-left: 54pt"><li><span style="color:#c00000">docker cp wordpress_wordpress_1:/var/www/html/wp-config.php wp-config.php</span>
		</li></ul><p><span style="font-family:Times New Roman; font-size:12pt">Edit the file with your preferred editor (I used Visual Studio Code), add the rows in blue: 
</span></p><p> 
 </p><p><span style="font-family:Courier New; font-size:8pt">&lt;?php<span style="color:black">
			</span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'DB_NAME'<span style="color:black">, <span style="color:#a31515">'wordpress'<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'DB_USER'<span style="color:black">, <span style="color:#a31515">'wordpress'<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'DB_PASSWORD'<span style="color:black">, <span style="color:#a31515">'bla bla bla'<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'DB_HOST'<span style="color:black">, <span style="color:#a31515">'db:3306'<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'DB_CHARSET'<span style="color:black">, <span style="color:#a31515">'utf8'<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'DB_COLLATE'<span style="color:black">, <span style="color:#a31515">''<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'AUTH_KEY'<span style="color:black">, <span style="color:#a31515">'bla bla bla'<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'SECURE_AUTH_KEY'<span style="color:black">, <span style="color:#a31515">'bla bla bla'<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'LOGGED_IN_KEY'<span style="color:black">, <span style="color:#a31515">'bla bla bla'<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'NONCE_KEY'<span style="color:black">, <span style="color:#a31515">'bla bla bla'<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'AUTH_SALT'<span style="color:black">, <span style="color:#a31515">'bla bla bla'<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'SECURE_AUTH_SALT'<span style="color:black">, <span style="color:#a31515">'bla bla bla'<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'LOGGED_IN_SALT'<span style="color:black">, <span style="color:#a31515">'bla bla bla'<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'NONCE_SALT'<span style="color:black">, <span style="color:#a31515">'bla bla bla'<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="font-family:Courier New; font-size:8pt"><span style="color:#00b0f0">define('JWT_AUTH_SECRET_KEY', 'bla bla bla'); </span>
		</span></p><p><span style="font-family:Courier New; font-size:8pt"><span style="color:#00b0f0">define('JWT_AUTH_CORS_ENABLE', true); </span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">$table_prefix = <span style="color:#a31515">'wp_'<span style="color:black">; </span>
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">define(<span style="color:#a31515">'WP_DEBUG'<span style="color:black">, <span style="color:blue">false<span style="color:black">); </span>
					</span></span></span></span></p><p><span style="color:green; font-family:Courier New; font-size:8pt">// If we're behind a proxy server and using HTTPS, we need to alert Wordpress of that fact<span style="color:black">
			</span>
		</span></p><p><span style="color:green; font-family:Courier New; font-size:8pt">// see also http://codex.wordpress.org/Administration_Over_SSL#Using_a_Reverse_Proxy<span style="color:black">
			</span>
		</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">if<span style="color:black"> (isset($_SERVER[<span style="color:#a31515">'HTTP_X_FORWARDED_PROTO'<span style="color:black">]) &amp;&amp; $_SERVER[<span style="color:#a31515">'HTTP_X_FORWARDED_PROTO'<span style="color:black">] === <span style="color:#a31515">'https'<span style="color:black">) { </span>
								</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">    $_SERVER[<span style="color:#a31515">'HTTPS'<span style="color:black">] = <span style="color:#a31515">'on'<span style="color:black">; </span>
					</span></span></span></span></p><p><span style="font-family:Courier New; font-size:8pt"><span style="color:black">}</span>
		</span></p><p><span style="color:green; font-family:Courier New; font-size:8pt">/* That's all, stop editing! Happy blogging. */<span style="color:black">
			</span>
		</span></p><p><span style="color:green; font-family:Courier New; font-size:8pt">/** Absolute path to the WordPress directory. */<span style="color:black">
			</span>
		</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">if<span style="color:black"> ( !defined(<span style="color:#a31515">'ABSPATH'<span style="color:black">) ) </span>
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">    define(<span style="color:#a31515">'ABSPATH'<span style="color:black">, dirname(<span style="color:blue">__FILE__<span style="color:black">) . <span style="color:#a31515">'/'<span style="color:black">); </span>
							</span></span></span></span></span></span></p><p><span style="color:green; font-family:Courier New; font-size:8pt">/** Sets up WordPress vars and included files. */<span style="color:black">
			</span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">require_once(ABSPATH . <span style="color:#a31515">'wp-settings.php'<span style="color:black">); </span>
			</span></span></p><p> 
 </p><p><span style="font-family:Times New Roman; font-size:12pt">Copy wp-config.php file from local Windows host to Docker container: 
</span></p><ul style="margin-left: 54pt"><li><span style="color:#c00000">docker cp wp-config.php wordpress_wordpress_1:/var/www/html/wp-config.php </span>
		</li></ul><p> 
 </p><p> 
 </p><h1>How to create blog posts from C# 
</h1><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System; </span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System.Collections.Generic; </span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System.Net.Http; </span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System.Net.Http.Headers; </span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System.Text; </span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> Newtonsoft.Json; </span></span>
		</span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">public<span style="color:black">
					<span style="color:blue">class<span style="color:black">
							<span style="color:#2b91af">TokenInfo<span style="color:black">
								</span></span></span></span></span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{ </span>
	</p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">    public<span style="color:black">
					<span style="color:blue">string<span style="color:black"> token { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; } </span></span></span></span></span></span></span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">public<span style="color:black">
					<span style="color:blue">string<span style="color:black"> user_email { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; } </span></span></span></span></span></span></span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">public<span style="color:black">
					<span style="color:blue">string<span style="color:black"> user_nicename { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; } </span></span></span></span></span></span></span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">public<span style="color:black">
					<span style="color:blue">string<span style="color:black"> user_display_name { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; } </span></span></span></span></span></span></span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">} </span>
	</p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">     using<span style="color:black"> (<span style="color:blue">var<span style="color:black"> client = <span style="color:blue">new<span style="color:black"> HttpClient()) </span></span></span></span></span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{ </span>
	</p><p><span style="color:black"><span style="font-family:Courier New; font-size:8pt">client.BaseAddress = <span style="color:blue">new<span style="color:black"> Uri(<span style="color:#a31515">"http://localhost:8000"<span style="color:black">); </span></span></span></span></span>
		</span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">string<span style="color:black"> loginInfo = <span style="color:maroon">@"{""username"": ""your-wordpress-user"", ""password"":""your-wordpress-password""}"<span style="color:black">; </span></span></span></span>
		</span></p><p> 
 </p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">var<span style="color:black"> tokenResponse = <span style="color:blue">await<span style="color:black"> client.PostAsync( </span></span></span></span>
		</span></p><p><span style="color:#a31515"><span style="font-family:Courier New; font-size:8pt">"/wp-json/jwt-auth/v1/token"<span style="color:black">, </span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">new<span style="color:black"> StringContent(loginInfo, Encoding.UTF8, <span style="color:#a31515">"application/json"<span style="color:black">)); </span></span></span></span>
		</span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">if<span style="color:black"> (tokenResponse.IsSuccessStatusCode) </span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{ </span>
	</p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">string<span style="color:black"> tokenAsText = <span style="color:blue">await<span style="color:black"> tokenResponse.Content.ReadAsStringAsync(); </span></span></span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">TokenInfo tokenInfo = JsonConvert.DeserializeObject&lt;TokenInfo&gt;(tokenAsText); </span>
	</p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">string<span style="color:black"> blogPost = <span style="color:maroon">@"{""title"": ""Blog post from C# - v2"", ""content"": ""&lt;div&gt;Just some content&lt;/div&gt;""}"<span style="color:black">; </span></span></span></span>
		</span></p><p><span style="color:black"><span style="font-family:Courier New; font-size:8pt">client.DefaultRequestHeaders.Authorization = <span style="color:blue">new<span style="color:black"> AuthenticationHeaderValue(<span style="color:#a31515">"Bearer"<span style="color:black">, tokenInfo.token); </span></span></span></span></span>
		</span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">var<span style="color:black"> createPostResponse = <span style="color:blue">await<span style="color:black"> client.PostAsync( </span></span></span></span>
		</span></p><p><span style="color:#a31515"><span style="font-family:Courier New; font-size:8pt">"/wp-json/wp/v2/posts"<span style="color:black">, </span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">new<span style="color:black"> StringContent(blogPost, Encoding.UTF8, <span style="color:#a31515">"application/json"<span style="color:black">)); </span></span></span></span>
		</span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">if<span style="color:black"> (createPostResponse.IsSuccessStatusCode) </span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{ </span>
	</p><p><span style="color:black"><span style="font-family:Courier New; font-size:8pt">Console.WriteLine(<span style="color:#a31515">"Success!"<span style="color:black">); </span></span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">} </span>
	</p><p><span style="color:black; font-family:Courier New; font-size:8pt">} </span>
	</p><p><span style="font-family:Courier New; font-size:8pt"><span style="color:black">}</span>
		</span>
	</p><p> 
 </p><p><span style="font-family:Times New Roman; font-size:12pt">Now this new post will be created, but it will not directly be visible, because it is created as draft. 
</span></p><p><span style="font-family:Times New Roman; font-size:12pt">To publish the post you will have to set the status to publish 
</span></p><p> 
 </p><h1>How to publish a draft post from C# 
</h1><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System; </span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System.Collections.Generic; </span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System.Net.Http; </span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System.Net.Http.Headers; </span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System.Text; </span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> Newtonsoft.Json; </span></span>
		</span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">public<span style="color:black">
					<span style="color:blue">class<span style="color:black">
							<span style="color:#2b91af">TokenInfo<span style="color:black">
								</span></span></span></span></span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{ </span>
	</p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">    public<span style="color:black">
					<span style="color:blue">string<span style="color:black"> token { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; } </span></span></span></span></span></span></span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">public<span style="color:black">
					<span style="color:blue">string<span style="color:black"> user_email { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; } </span></span></span></span></span></span></span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">public<span style="color:black">
					<span style="color:blue">string<span style="color:black"> user_nicename { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; } </span></span></span></span></span></span></span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">public<span style="color:black">
					<span style="color:blue">string<span style="color:black"> user_display_name { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; } </span></span></span></span></span></span></span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">} </span>
	</p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> (<span style="color:blue">var<span style="color:black"> client = <span style="color:blue">new<span style="color:black"> HttpClient()) </span></span></span></span></span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{ </span>
	</p><p><span style="color:black"><span style="font-family:Courier New; font-size:8pt">client.BaseAddress = <span style="color:blue">new<span style="color:black"> Uri(<span style="color:#a31515">"http://localhost:8000"<span style="color:black">); </span></span></span></span></span>
		</span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">string<span style="color:black"> loginInfo = <span style="color:maroon">@"{""username"": ""your-wordpress-user"", ""password"":""your-wordpress-password""}"<span style="color:black">; </span></span></span></span>
		</span></p><p> 
 </p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">var<span style="color:black"> tokenResponse = <span style="color:blue">await<span style="color:black"> client.PostAsync( </span></span></span></span>
		</span></p><p><span style="color:#a31515"><span style="font-family:Courier New; font-size:8pt">"/wp-json/jwt-auth/v1/token"<span style="color:black">, </span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">new<span style="color:black"> StringContent(loginInfo, Encoding.UTF8, <span style="color:#a31515">"application/json"<span style="color:black">)); </span></span></span></span>
		</span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">if<span style="color:black"> (tokenResponse.IsSuccessStatusCode) </span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{ </span>
	</p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">string<span style="color:black"> tokenAsText = <span style="color:blue">await<span style="color:black"> tokenResponse.Content.ReadAsStringAsync(); </span></span></span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">TokenInfo tokenInfo = JsonConvert.DeserializeObject&lt;TokenInfo&gt;(tokenAsText); </span>
	</p><p><span style="color:black"><span style="font-family:Courier New; font-size:8pt">client.DefaultRequestHeaders.Authorization = <span style="color:blue">new<span style="color:black"> AuthenticationHeaderValue(<span style="color:#a31515">"Bearer"<span style="color:black">, tokenInfo.token); </span></span></span></span></span>
		</span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">string<span style="color:black"> blogPost = <span style="color:maroon">@"{""status"": ""publish""}"<span style="color:black">; </span></span></span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">int<span style="color:black"> blogPostId = 8; // This is the ID for the draft blogpost you want to publish. </span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">string<span style="color:black"> blogPostUpdateUrl = <span style="color:#a31515">$"/wp-json/wp/v2/posts/<span style="color:black">{blogPostId}<span style="color:#a31515">"<span style="color:black">; </span></span></span></span></span></span>
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">var<span style="color:black"> createPostResponse = <span style="color:blue">await<span style="color:black"> client.PostAsync( </span></span></span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">blogPostUpdateUrl, </span>
	</p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">new<span style="color:black"> StringContent(blogPost, Encoding.UTF8, <span style="color:#a31515">"application/json"<span style="color:black">)); </span></span></span></span>
		</span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">if<span style="color:black"> (createPostResponse.IsSuccessStatusCode) </span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{ </span>
	</p><p><span style="color:black"><span style="font-family:Courier New; font-size:8pt">Console.WriteLine(<span style="color:#a31515">"Success!"<span style="color:black">); </span></span></span>
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">} </span>
	</p><p><span style="color:black; font-family:Courier New; font-size:8pt">} </span>
	</p><p><span style="color:black"><span style="font-family:Courier New; font-size:8pt">Assert.AreEqual(<span style="color:blue">true<span style="color:black">, <span style="color:blue">true<span style="color:black">); </span></span></span></span></span>
		</span></p><p><span style="font-family:Courier New; font-size:8pt"><span style="color:black">}</span>
		</span>
	</p><p> 
 </p><p> 
 </p><p> 
 </p><h1>How to get all draft posts from C# 
</h1><p><span style="font-family:Times New Roman; font-size:12pt">To get all draft posts from C# you must be authenticated so use the following code: 
</span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System; </span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System.Collections.Generic; </span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System.Net.Http; </span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System.Net.Http.Headers; </span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> System.Text; </span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> Newtonsoft.Json; </span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">public<span style="color:black">
					<span style="color:blue">class<span style="color:black">
							<span style="color:#2b91af">TokenInfo<span style="color:black">
								</span></span></span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{ </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">    public<span style="color:black">
					<span style="color:blue">string<span style="color:black"> token { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; } </span></span></span></span></span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">public<span style="color:black">
					<span style="color:blue">string<span style="color:black"> user_email { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; } </span></span></span></span></span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">public<span style="color:black">
					<span style="color:blue">string<span style="color:black"> user_nicename { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; } </span></span></span></span></span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">public<span style="color:black">
					<span style="color:blue">string<span style="color:black"> user_display_name { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; } </span></span></span></span></span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">} </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p> 
 </p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">using<span style="color:black"> (<span style="color:blue">var<span style="color:black"> client = <span style="color:blue">new<span style="color:black"> HttpClient()) </span></span></span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{ </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:black"><span style="font-family:Courier New; font-size:8pt">client.BaseAddress = <span style="color:blue">new<span style="color:black"> Uri(<span style="color:#a31515">"http://localhost:8000"<span style="color:black">); </span></span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">string<span style="color:black"> loginInfo = <span style="color:maroon">@"{""username"": ""your-wordpress-user"", ""password"":""your-wordpress-password""}"<span style="color:black">; </span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p> 
 </p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">var<span style="color:black"> tokenResponse = <span style="color:blue">await<span style="color:black"> client.PostAsync( </span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:#a31515"><span style="font-family:Courier New; font-size:8pt">"/wp-json/jwt-auth/v1/token"<span style="color:black">, </span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">new<span style="color:black"> StringContent(loginInfo, Encoding.UTF8, <span style="color:#a31515">"application/json"<span style="color:black">)); </span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">if<span style="color:black"> (tokenResponse.IsSuccessStatusCode) </span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{ </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">string<span style="color:black"> tokenAsText = <span style="color:blue">await<span style="color:black"> tokenResponse.Content.ReadAsStringAsync(); </span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">TokenInfo tokenInfo = JsonConvert.DeserializeObject&lt;TokenInfo&gt;(tokenAsText); </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:black"><span style="font-family:Courier New; font-size:8pt">client.DefaultRequestHeaders.Authorization = <span style="color:blue">new<span style="color:black"> AuthenticationHeaderValue(<span style="color:#a31515">"Bearer"<span style="color:black">, tokenInfo.token); </span></span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">var<span style="color:black"> response = <span style="color:blue">await<span style="color:black"> client.GetAsync(<span style="color:#a31515">"/wp-json/wp/v2/posts?status=draft"<span style="color:black">); </span></span></span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p> 
 </p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">if<span style="color:black"> (response.IsSuccessStatusCode) </span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{ </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">string<span style="color:black"> postsAsText = <span style="color:blue">await<span style="color:black"> response.Content.ReadAsStringAsync(); </span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">List&lt;WpPost&gt; draftPosts = JsonConvert.DeserializeObject&lt;List&lt;WpPost&gt;&gt;(postsAsText); </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:blue"><span style="font-family:Courier New; font-size:8pt">foreach<span style="color:black"> (WpPost post <span style="color:blue">in<span style="color:black"> draftPosts) </span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{ </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:black"><span style="font-family:Courier New; font-size:8pt">Console.WriteLine(<span style="color:#a31515">$"tile [<span style="color:black">{post.title}<span style="color:#a31515">]"<span style="color:black">); </span></span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">} </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">} </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p> 
 </p><p><span style="color:black; font-family:Courier New; font-size:8pt">} </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:black"><span style="font-family:Courier New; font-size:8pt">Assert.AreEqual(<span style="color:blue">true<span style="color:black">, <span style="color:blue">true<span style="color:black">); </span></span></span></span></span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p><span style="font-family:Courier New; font-size:8pt"><span style="color:black">}</span>
		</span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p> 
 </p><p><span style="font-family:Times New Roman; font-size:12pt">Note : I used http://json2csharp.com to convert JSON to C# classes to get a type safe response from the server. 
</span></p><p><span style="font-family:Times New Roman; font-size:12pt">The following code is generated by http://json2csharp.com 
</span></p><p><span style="font-family:Courier New; font-size:8pt"> <span style="color:blue">public<span style="color:black">
					<span style="color:blue">class<span style="color:black">
							<span style="color:#2b91af">WpGuid<span style="color:black">
								</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> rendered { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">class<span style="color:black">
						<span style="color:#2b91af">Title<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> rendered { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">class<span style="color:black">
						<span style="color:#2b91af">Content<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> rendered { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">bool<span style="color:black"> @protected { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">class<span style="color:black">
						<span style="color:#2b91af">Excerpt<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> rendered { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">bool<span style="color:black"> @protected { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">class<span style="color:black">
						<span style="color:#2b91af">Self<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> href { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">class<span style="color:black">
						<span style="color:#2b91af">Collection<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> href { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">class<span style="color:black">
						<span style="color:#2b91af">About<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> href { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">class<span style="color:black">
						<span style="color:#2b91af">Author<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">bool<span style="color:black"> embeddable { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> href { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">class<span style="color:black">
						<span style="color:#2b91af">Reply<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">bool<span style="color:black"> embeddable { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> href { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">class<span style="color:black">
						<span style="color:#2b91af">VersionHistory<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> href { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">class<span style="color:black">
						<span style="color:#2b91af">WpAttachment<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> href { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">class<span style="color:black">
						<span style="color:#2b91af">WpTerm<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> taxonomy { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">bool<span style="color:black"> embeddable { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> href { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">class<span style="color:black">
						<span style="color:#2b91af">Cury<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> name { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> href { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">bool<span style="color:black"> templated { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">class<span style="color:black">
						<span style="color:#2b91af">Links<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> List&lt;Self&gt; self { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> List&lt;Collection&gt; collection { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> List&lt;About&gt; about { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> List&lt;Author&gt; author { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> List&lt;Reply&gt; replies { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> List&lt;Cury&gt; curies { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">class<span style="color:black">
						<span style="color:#2b91af">WpPost<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:8pt">{
</span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">int<span style="color:black"> id { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> DateTime date { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> DateTime date_gmt { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> WpGuid guid { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> DateTime modified { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> DateTime modified_gmt { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> slug { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> status { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> type { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> link { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> Title title { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> Content content { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> Excerpt excerpt { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">int<span style="color:black"> author { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">int<span style="color:black"> featured_media { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> comment_status { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> ping_status { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">bool<span style="color:black"> sticky { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> template { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black">
				<span style="color:blue">string<span style="color:black"> format { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> List&lt;<span style="color:blue">object<span style="color:black">&gt; meta { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> List&lt;<span style="color:blue">int<span style="color:black">&gt; categories { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> List&lt;<span style="color:blue">object<span style="color:black">&gt; tags { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:8pt">public<span style="color:black"> Links _links { <span style="color:blue">get<span style="color:black">; <span style="color:blue">set<span style="color:black">; }
</span></span></span></span></span></span></p><p><span style="font-family:Courier New; font-size:8pt"><span style="color:black">}</span>
		</span></p><p> 
 </p><p> 
 </p><p> 
 </p><p> 
 </p><p><span style="font-family:Times New Roman; font-size:12pt"> </span> </p>