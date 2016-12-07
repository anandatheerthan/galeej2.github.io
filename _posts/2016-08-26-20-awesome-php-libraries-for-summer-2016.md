---
layout: post
title: 20 Awesome PHP Libraries For Summer 2016
date: 2016-08-26 14:28
author: administrator
comments: true
categories: [Laravel, Laravel, PHP, php]
---
<h3><a href="https://github.com/Seldaek/monolog" target="_blank">Monolog</a></h3>
With Monolog you can create advanced logging systems by sending your PHP logs to files, sockets, databases, inboxes or other web services. The library has over 50 handlers for various utilities and can be integrated into frameworks such as Laravel, Symfony2 and Slim.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
"><code class="php hljs"><span class="hljs-keyword">use</span> <span class="hljs-title">Monolog</span>\<span class="hljs-title">Logger</span>;
<span class="hljs-keyword">use</span> <span class="hljs-title">Monolog</span>\<span class="hljs-title">Handler</span>\<span class="hljs-title">StreamHandler</span>;

<span class="hljs-comment">// create a log channel</span>
<span class="hljs-variable">$log</span> = <span class="hljs-keyword">new</span> Logger(<span class="hljs-string">'name'</span>);
<span class="hljs-variable">$log</span>-&gt;pushHandler(<span class="hljs-keyword">new</span> StreamHandler(<span class="hljs-string">'path/to/your.log'</span>, Logger::WARNING));

<span class="hljs-comment">// add records to the log</span>
<span class="hljs-variable">$log</span>-&gt;warning(<span class="hljs-string">'Foo'</span>);
<span class="hljs-variable">$log</span>-&gt;error(<span class="hljs-string">'Bar'</span>);</code></pre>

<hr />

<h3><a href="https://github.com/PHPOffice/PHPExcel" target="_blank">PHPExcel</a></h3>
A set of PHP classes that allow developers to easily implement spreadsheet editing in their apps. The library can read and write spreadsheet documents in a number of popular formats including Excel (both .xls and .xlsx), OpenDocument (.ods), and CSV to name a few.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
"><code class="php hljs"><span class="hljs-keyword">include</span> <span class="hljs-string">'PHPExcel/IOFactory.php'</span>;

<span class="hljs-variable">$inputFileName</span> = <span class="hljs-string">'./sampleData/example1.xls'</span>;

<span class="hljs-keyword">echo</span> <span class="hljs-string">'Loading file '</span>,pathinfo(<span class="hljs-variable">$inputFileName</span>,PATHINFO_BASENAME),<span class="hljs-string">' using IOFactory'</span>;
<span class="hljs-variable">$objPHPExcel</span> = PHPExcel_IOFactory::load(<span class="hljs-variable">$inputFileName</span>);

<span class="hljs-variable">$sheetData</span> = <span class="hljs-variable">$objPHPExcel</span>-&gt;getActiveSheet()-&gt;toArray(<span class="hljs-keyword">null</span>,<span class="hljs-keyword">true</span>,<span class="hljs-keyword">true</span>,<span class="hljs-keyword">true</span>);
var_dump(<span class="hljs-variable">$sheetData</span>);</code></pre>

<hr />

<h3><a href="https://github.com/php-ai/php-ml" target="_blank">PHP-ML</a></h3>
An interesting library for experimenting with Machine Learning, PHP-ML gives you an easy to use API for training your bot and making it do predictions based on input data. It offers a variety of different algorithms for pattern recognition and complex statistics calculations.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
"><code class="php hljs"><span class="hljs-keyword">use</span> <span class="hljs-title">Phpml</span>\<span class="hljs-title">Classification</span>\<span class="hljs-title">KNearestNeighbors</span>;

<span class="hljs-variable">$samples</span> = [[<span class="hljs-number">1</span>, <span class="hljs-number">3</span>], [<span class="hljs-number">1</span>, <span class="hljs-number">4</span>], [<span class="hljs-number">2</span>, <span class="hljs-number">4</span>], [<span class="hljs-number">3</span>, <span class="hljs-number">1</span>], [<span class="hljs-number">4</span>, <span class="hljs-number">1</span>], [<span class="hljs-number">4</span>, <span class="hljs-number">2</span>]];
<span class="hljs-variable">$labels</span> = [<span class="hljs-string">'a'</span>, <span class="hljs-string">'a'</span>, <span class="hljs-string">'a'</span>, <span class="hljs-string">'b'</span>, <span class="hljs-string">'b'</span>, <span class="hljs-string">'b'</span>];

<span class="hljs-variable">$classifier</span> = <span class="hljs-keyword">new</span> KNearestNeighbors();
<span class="hljs-variable">$classifier</span>-&gt;train(<span class="hljs-variable">$samples</span>, <span class="hljs-variable">$labels</span>);

<span class="hljs-variable">$classifier</span>-&gt;predict([<span class="hljs-number">3</span>, <span class="hljs-number">2</span>]);
<span class="hljs-comment">// returns 'b' as the [3, 2] point is closer to the points in group b</span></code></pre>

<hr />

<h3><a href="https://github.com/opauth/opauth" target="_blank">Opauth</a></h3>
Library for enabling users to authenticate themselves via their account in social networks or other services. Of course all the big names are available: Google, Facebook, Twitter, Github, Instagram, LinkedIn. Opauth is supported by many PHP frameworks so it can be easily integrated in most PHP apps.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
"><code class="php hljs"><span class="hljs-string">'Strategy'</span> =&gt; <span class="hljs-keyword">array</span>(  
    <span class="hljs-comment">// Define strategies here.</span>

    <span class="hljs-string">'Facebook'</span> =&gt; <span class="hljs-keyword">array</span>(
        <span class="hljs-string">'app_id'</span> =&gt; <span class="hljs-string">'YOUR APP ID'</span>,
        <span class="hljs-string">'app_secret'</span> =&gt; <span class="hljs-string">'YOUR APP SECRET'</span>
    ),
);</code></pre>

<hr />

<h3><a href="https://github.com/filp/whoops" target="_blank">Whoops</a></h3>
Whoops greatly improves the debugging experience in PHP by displaying a detailed error page when something breaks in an app. This error page gives us the full stack trace showing the specific files and snippets of code that caused the exception, all syntax-highlighted and colorful. The Laravel framework comes with Whoops built-in.
<pre class="brush:php" data-lines="1
2
3
4
"><code class="php hljs"><span class="hljs-variable">$whoops</span> = <span class="hljs-keyword">new</span> \Whoops\Run;
<span class="hljs-variable">$whoops</span>-&gt;pushHandler(<span class="hljs-keyword">new</span> \Whoops\Handler\PrettyPageHandler);
<span class="hljs-variable">$whoops</span>-&gt;register();
<span class="hljs-comment">// That's it!</span></code></pre>

<hr />

<h3><a href="https://github.com/PHPSocialNetwork/phpfastcache" target="_blank">FastCache</a></h3>
Implementing this caching system in your PHP apps is guaranteed to make them load way quicker by reducing the amount of queries sent to the database. Instead of executing every DB query, FastCache sends only the unique ones, saves them as cache, and then serves them from there for each repetition. This way if you have the same query repeated 1000 times, it will be loaded from the DB one time, the rest 999 loads will be from cache.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
"><code class="php hljs"><span class="hljs-keyword">use</span> <span class="hljs-title">phpFastCache</span>\<span class="hljs-title">CacheManager</span>;

<span class="hljs-variable">$config</span> = <span class="hljs-keyword">array</span>(
    <span class="hljs-string">"storage"</span>   =&gt;  <span class="hljs-string">"files"</span>,
    <span class="hljs-string">"path"</span>      =&gt;  <span class="hljs-string">"/your_cache_path/dir/"</span>,
);
CacheManager::setup(<span class="hljs-variable">$config</span>);

<span class="hljs-comment">// Try to get from Cache first with an Identity Keyword</span>
<span class="hljs-variable">$products</span> = CacheManager::get(<span class="hljs-string">"products"</span>);

<span class="hljs-comment">// If not available get from DB and save in Cache.</span>
<span class="hljs-keyword">if</span>(is_null(<span class="hljs-variable">$products</span>)) {
    <span class="hljs-variable">$products</span> = <span class="hljs-string">"DB SELECT QUERY"</span>;
    <span class="hljs-comment">// Cache your $products for 600 seconds.</span>
    CacheManager::set(<span class="hljs-variable">$cache_keyword</span>, <span class="hljs-variable">$products</span>,<span class="hljs-number">600</span>);
}</code></pre>

<hr />

<h3><a href="https://github.com/guzzle/guzzle" target="_blank">Guzzle</a></h3>
Guzzle is one of the best HTTP clients out there. It can handle almost any HTTP task that you throw at it: synchronous and asynchronous requests, HTTP cookies, streaming of large uploads and downloads. Working with Guzzle is really easy and the docs are well written with lots of examples and detailed explanations.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
"><code class="php hljs"><span class="hljs-variable">$client</span> = <span class="hljs-keyword">new</span> GuzzleHttp\Client();
<span class="hljs-variable">$res</span> = <span class="hljs-variable">$client</span>-&gt;request(<span class="hljs-string">'GET'</span>, <span class="hljs-string">'https://api.github.com/user'</span>, [
    <span class="hljs-string">'auth'</span> =&gt; [<span class="hljs-string">'user'</span>, <span class="hljs-string">'pass'</span>]
]);
<span class="hljs-keyword">echo</span> <span class="hljs-variable">$res</span>-&gt;getStatusCode();
<span class="hljs-comment">// "200"</span>
<span class="hljs-keyword">echo</span> <span class="hljs-variable">$res</span>-&gt;getHeader(<span class="hljs-string">'content-type'</span>);
<span class="hljs-comment">// 'application/json; charset=utf8'</span>
<span class="hljs-keyword">echo</span> <span class="hljs-variable">$res</span>-&gt;getBody();
<span class="hljs-comment">// {"type":"User"...'</span>

<span class="hljs-comment">// Send an asynchronous request.</span>
<span class="hljs-variable">$request</span> = <span class="hljs-keyword">new</span> \GuzzleHttp\Psr7\Request(<span class="hljs-string">'GET'</span>, <span class="hljs-string">'http://httpbin.org'</span>);
<span class="hljs-variable">$promise</span> = <span class="hljs-variable">$client</span>-&gt;sendAsync(<span class="hljs-variable">$request</span>)-&gt;then(<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-params">(<span class="hljs-variable">$response</span>)</span> </span>{
    <span class="hljs-keyword">echo</span> <span class="hljs-string">'I completed! '</span> . <span class="hljs-variable">$response</span>-&gt;getBody();
});
<span class="hljs-variable">$promise</span>-&gt;wait();</code></pre>

<hr />

<h3><a href="https://github.com/meenie/munee" target="_blank">Munee</a></h3>
Munee has lots of tricks up its sleeve: combining several CSS or JavaScript requests into one, image resizing, automatic compilation for Sass, Less and CoffeeScript files, as well as minification and Gzip compression. All of the previously mentioned processes are cached both server-side and client-side for optimal performance.
<pre class="brush:php" data-lines="1
2
"><code class="php hljs"><span class="hljs-keyword">require</span> <span class="hljs-string">'vendor/autoload.php'</span>;
<span class="hljs-keyword">echo</span> \Munee\Dispatcher::run(<span class="hljs-keyword">new</span> \Munee\Request());</code></pre>
<pre class="brush:html" data-lines="1
2
3
4
5
6
7
8
9
10
11
"><code class="html hljs xml"><span class="hljs-comment">&lt;!-- Combining two CSS files into one. --&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-title">link</span> <span class="hljs-attribute">rel</span>=<span class="hljs-value">"stylesheet"</span> <span class="hljs-attribute">href</span>=<span class="hljs-value">"/css/bootstrap.min.css, /css/demo.css"</span>&gt;</span>

<span class="hljs-comment">&lt;!-- Resizing image --&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-title">img</span> <span class="hljs-attribute">src</span>=<span class="hljs-value">"/path/to/image.jpg?resize=width[100]height[100]exact[true]"</span>&gt;</span>

<span class="hljs-comment">&lt;!-- Files that need preprocessing are compiled automatically --&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-title">link</span> <span class="hljs-attribute">rel</span>=<span class="hljs-value">"stylesheet"</span> <span class="hljs-attribute">href</span>=<span class="hljs-value">"/css/demo.scss"</span>&gt;</span>

<span class="hljs-comment">&lt;!-- Minifying code --&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-title">script</span> <span class="hljs-attribute">src</span>=<span class="hljs-value">"/js/script.js?minify=true"</span>&gt;</span><span class="hljs-tag">&lt;/<span class="hljs-title">script</span>&gt;</span></code></pre>

<hr />

<h3><a href="https://github.com/twigphp/Twig" target="_blank">Twig</a></h3>
Templating engine with a very clean “mustache” syntax that makes markup shorter and easier to write. Twig offers everything you would expect from a modern templating library: variable escaping, loops, if/else blocks, as well as a secure sandbox mode for verifying template code.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
"><code class="php hljs"><span class="hljs-comment">// Template HTML</span>

&lt;p&gt;Welcome {{ name }}!&lt;/p&gt;


<span class="hljs-comment">// Rendering</span>

<span class="hljs-keyword">require_once</span> <span class="hljs-string">'/path/to/lib/Twig/Autoloader.php'</span>;
Twig_Autoloader::register();

<span class="hljs-variable">$loader</span> = <span class="hljs-keyword">new</span> Twig_Loader_Filesystem(<span class="hljs-string">'/path/to/templates'</span>);
<span class="hljs-variable">$twig</span> = <span class="hljs-keyword">new</span> Twig_Environment(<span class="hljs-variable">$loader</span>, <span class="hljs-keyword">array</span>(
    <span class="hljs-string">'cache'</span> =&gt; <span class="hljs-string">'/path/to/compilation_cache'</span>,
));

<span class="hljs-keyword">echo</span> <span class="hljs-variable">$twig</span>-&gt;render(<span class="hljs-string">'index.html'</span>, <span class="hljs-keyword">array</span>(<span class="hljs-string">'name'</span> =&gt; <span class="hljs-string">'George'</span>));</code></pre>

<hr />

<h3><a href="https://github.com/FriendsOfPHP/Goutte" target="_blank">Goutte</a></h3>
Goutte is a Web Scraper that can crawl websites and extract HTML or XML data from them. It works by sending a request to a given URL and returning a Crawler object, which allows the developer to interact with the remote page in various ways.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
11
12
13
14
"><code class="php hljs"><span class="hljs-keyword">use</span> <span class="hljs-title">Goutte</span>\<span class="hljs-title">Client</span>;
<span class="hljs-variable">$client</span> = <span class="hljs-keyword">new</span> Client();

<span class="hljs-comment">// Go to the symfony.com website</span>
<span class="hljs-variable">$crawler</span> = <span class="hljs-variable">$client</span>-&gt;request(<span class="hljs-string">'GET'</span>, <span class="hljs-string">'http://www.symfony.com/blog/'</span>);

<span class="hljs-comment">// Click on the links</span>
<span class="hljs-variable">$link</span> = <span class="hljs-variable">$crawler</span>-&gt;selectLink(<span class="hljs-string">'Security Advisories'</span>)-&gt;link();
<span class="hljs-variable">$crawler</span> = <span class="hljs-variable">$client</span>-&gt;click(<span class="hljs-variable">$link</span>);

<span class="hljs-comment">// Extract data</span>
<span class="hljs-variable">$crawler</span>-&gt;filter(<span class="hljs-string">'h2 &gt; a'</span>)-&gt;each(<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-params">(<span class="hljs-variable">$node</span>)</span> </span>{
    <span class="hljs-keyword">print</span> <span class="hljs-variable">$node</span>-&gt;text().<span class="hljs-string">"\n"</span>;
});</code></pre>
<div class="gad hide600 adsbygoogle"><ins class="adsbygoogle" data-ad-client="ca-pub-4243460155472587" data-ad-slot="5272744153" data-adsbygoogle-status="done"><ins id="aswift_2_expand"><ins id="aswift_2_anchor"><iframe width="336" height="280" frameborder="0" marginwidth="0" marginheight="0" vspace="0" hspace="0" allowtransparency="true" scrolling="no" allowfullscreen="allowfullscreen" onload="var i=this.id,s=window.google_iframe_oncopy,H=s&amp;&amp;s.handlers,h=H&amp;&amp;H[i],w=this.contentWindow,d;try{d=w.document}catch(e){}if(h&amp;&amp;d&amp;&amp;(!d.body||!d.body.firstChild)){if(h.call){setTimeout(h,0)}else if(h.match){try{h=s.upd(h,i)}catch(e){}w.location.replace(h)}}" id="aswift_2" name="aswift_2"></iframe></ins></ins></ins></div>

<hr />

<h3><a href="https://github.com/thephpleague/climate" target="_blank">Climate</a></h3>
Climate is a library for people who run PHP from the command line. It offers a collection of methods for talking to the terminal (both input and output), and also some beautifying functions for coloring and formatting. It can even draw and animate cool ASCII art.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
"><code class="php hljs"><span class="hljs-variable">$climate</span> = <span class="hljs-keyword">new</span> League\CLImate\CLImate;

<span class="hljs-comment">// Output</span>
<span class="hljs-variable">$climate</span>-&gt;out(<span class="hljs-string">'This prints to the terminal.'</span>);

<span class="hljs-comment">// Input</span>
<span class="hljs-variable">$input</span> = <span class="hljs-variable">$climate</span>-&gt;input(<span class="hljs-string">'How you doin?'</span>);
<span class="hljs-variable">$response</span> = <span class="hljs-variable">$input</span>-&gt;prompt();

<span class="hljs-comment">// Formatting</span>
<span class="hljs-variable">$padding</span> = <span class="hljs-variable">$climate</span>-&gt;padding(<span class="hljs-number">10</span>);

<span class="hljs-variable">$padding</span>-&gt;label(<span class="hljs-string">'Eggs'</span>)-&gt;result(<span class="hljs-string">'$1.99'</span>);
<span class="hljs-variable">$padding</span>-&gt;label(<span class="hljs-string">'Oatmeal'</span>)-&gt;result(<span class="hljs-string">'$4.99'</span>);
<span class="hljs-comment">// Eggs...... $1.99</span>
<span class="hljs-comment">// Oatmeal... $4.99</span></code></pre>

<hr />

<h3><a href="https://github.com/nelmio/alice" target="_blank">Alice</a></h3>
Built on top of <a href="https://github.com/fzaninotto/Faker" target="_blank">Faker</a>, Alice is a library that generates fake data objects for testing. To use it you first have to define the structure of your objects and what data you want in them. Then with a simple function call Alice will transform this template into an actual object with random values.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
11
"><code class="php hljs"><span class="hljs-comment">// Template in person.yml file</span>
Person:
    person{<span class="hljs-number">1.</span>.<span class="hljs-number">10</span>}:
        firstName: <span class="hljs-string">'&lt;firstName()&gt;'</span>
        lastName: <span class="hljs-string">'&lt;lastName()&gt;'</span>
        birthDate: <span class="hljs-string">'&lt;date()&gt;'</span>
        email: <span class="hljs-string">'&lt;email()&gt;'</span>


<span class="hljs-comment">// Load dummy data into an object</span>
<span class="hljs-variable">$person</span> = \Nelmio\Alice\Fixtures::load(<span class="hljs-string">'/person.yml'</span>, <span class="hljs-variable">$objectManager</span>);</code></pre>

<hr />

<h3><a href="https://github.com/ratchetphp/Ratchet/" target="_blank">Ratchet</a></h3>
The Ratchet library adds support for the <a href="https://en.wikipedia.org/wiki/WebSocket" target="_blank">WebSockets</a> interface in apps with a PHP backend. WebSockets enable two-way communication between the server and client side in real time. For this to work in PHP, Ratchet has to start a separate PHP process that stays always running and asynchronously sends and receives messages.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
"><code class="php hljs"><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">MyChat</span> <span class="hljs-keyword">implements</span> <span class="hljs-title">MessageComponentInterface</span> </span>{
    <span class="hljs-keyword">protected</span> <span class="hljs-variable">$clients</span>;

    <span class="hljs-keyword">public</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">__construct</span><span class="hljs-params">()</span> </span>{
        <span class="hljs-variable">$this</span>-&gt;clients = <span class="hljs-keyword">new</span> \SplObjectStorage;
    }

    <span class="hljs-keyword">public</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">onOpen</span><span class="hljs-params">(ConnectionInterface <span class="hljs-variable">$conn</span>)</span> </span>{
        <span class="hljs-variable">$this</span>-&gt;clients-&gt;attach(<span class="hljs-variable">$conn</span>);
    }

    <span class="hljs-keyword">public</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">onMessage</span><span class="hljs-params">(ConnectionInterface <span class="hljs-variable">$from</span>, <span class="hljs-variable">$msg</span>)</span> </span>{
        <span class="hljs-keyword">foreach</span> (<span class="hljs-variable">$this</span>-&gt;clients <span class="hljs-keyword">as</span> <span class="hljs-variable">$client</span>) {
            <span class="hljs-keyword">if</span> (<span class="hljs-variable">$from</span> != <span class="hljs-variable">$client</span>) {
                <span class="hljs-variable">$client</span>-&gt;send(<span class="hljs-variable">$msg</span>);
            }
        }
    }
}

<span class="hljs-comment">// Run the server application through the WebSocket protocol on port 8080</span>
<span class="hljs-variable">$app</span> = <span class="hljs-keyword">new</span> Ratchet\App(<span class="hljs-string">'localhost'</span>, <span class="hljs-number">8080</span>);
<span class="hljs-variable">$app</span>-&gt;route(<span class="hljs-string">'/chat'</span>, <span class="hljs-keyword">new</span> MyChat);
<span class="hljs-variable">$app</span>-&gt;run();</code></pre>

<hr />

<h3><a href="https://github.com/PHPMailer/PHPMailer" target="_blank">PHPMailer</a></h3>
No PHP library collection is complete without PHPMailer. This project is backed by a huge community and is implemented in popular systems such as WordPress and Drupal, making it the safest choice for sending emails in PHP. It has <a href="https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol" target="_blank">SMTP</a> support, can do HTML-based emails, and much more.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
"><code class="php hljs"><span class="hljs-keyword">require</span> <span class="hljs-string">'PHPMailerAutoload.php'</span>;

<span class="hljs-variable">$mail</span> = <span class="hljs-keyword">new</span> PHPMailer;

<span class="hljs-variable">$mail</span>-&gt;setFrom(<span class="hljs-string">'from@example.com'</span>, <span class="hljs-string">'Mailer'</span>);
<span class="hljs-variable">$mail</span>-&gt;addAddress(<span class="hljs-string">'steve@example.com'</span>);    

<span class="hljs-variable">$mail</span>-&gt;addAttachment(<span class="hljs-string">'/var/tmp/file.tar.gz'</span>);        
<span class="hljs-variable">$mail</span>-&gt;isHTML(<span class="hljs-keyword">true</span>);                                  

<span class="hljs-variable">$mail</span>-&gt;Subject = <span class="hljs-string">'Here is the subject'</span>;
<span class="hljs-variable">$mail</span>-&gt;Body    = <span class="hljs-string">'This is the HTML message body &lt;b&gt;in bold!&lt;/b&gt;'</span>;

<span class="hljs-keyword">if</span>(!<span class="hljs-variable">$mail</span>-&gt;send()) {
    <span class="hljs-keyword">echo</span> <span class="hljs-string">'Message could not be sent.'</span>;
    <span class="hljs-keyword">echo</span> <span class="hljs-string">'Mailer Error: '</span> . <span class="hljs-variable">$mail</span>-&gt;ErrorInfo;
} <span class="hljs-keyword">else</span> {
    <span class="hljs-keyword">echo</span> <span class="hljs-string">'Message has been sent'</span>;
}</code></pre>

<hr />

<h3><a href="http://hoa-project.net/En/" target="_blank">Hoa</a></h3>
Hoa isn’t actually a PHP library – it’s an entire set of PHP libraries, containing all kinds of useful web development utilities. Although not all are fully documented, there are 50+ libraries right now, with new ones constantly being added. It’s completely modular so you can select only the libraries you need without any clutter.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
"><code class="php hljs"><span class="hljs-comment">// Hoa Mail</span>
<span class="hljs-variable">$message</span>            = <span class="hljs-keyword">new</span> Hoa\Mail\Message();
<span class="hljs-variable">$message</span>[<span class="hljs-string">'From'</span>]    = <span class="hljs-string">'Gordon Freeman &lt;gordon@freeman.hf&gt;'</span>;
<span class="hljs-variable">$message</span>[<span class="hljs-string">'To'</span>]      = <span class="hljs-string">'Alyx Vance &lt;alyx@vance.hf&gt;'</span>;
<span class="hljs-variable">$message</span>[<span class="hljs-string">'Subject'</span>] = <span class="hljs-string">'Hoa is awesome!'</span>;
<span class="hljs-variable">$message</span>-&gt;addContent(
    <span class="hljs-keyword">new</span> Hoa\Mail\Content\Text(<span class="hljs-string">'Check this out: http://hoa-project.net/!'</span>)
);
<span class="hljs-variable">$message</span>-&gt;send();

<span class="hljs-comment">// Hoa Session</span>
<span class="hljs-variable">$user</span> = <span class="hljs-keyword">new</span> Hoa\Session\Session(<span class="hljs-string">'user'</span>);

<span class="hljs-keyword">if</span> (<span class="hljs-variable">$user</span>-&gt;isEmpty()) {
    <span class="hljs-keyword">echo</span> <span class="hljs-string">'first time'</span>, <span class="hljs-string">"\n"</span>;
    <span class="hljs-variable">$user</span>[<span class="hljs-string">'foo'</span>] = time();
} <span class="hljs-keyword">else</span> {
    <span class="hljs-keyword">echo</span> <span class="hljs-string">'other times'</span>, <span class="hljs-string">"\n"</span>;
    var_dump(<span class="hljs-variable">$user</span>[<span class="hljs-string">'foo'</span>]);
}</code></pre>

<hr />

<h3><a href="https://github.com/tijsverkoyen/CssToInlineStyles" target="_blank">CssToInlineStyles</a></h3>
Anyone who has tried creating HTML emails knows what a pain it is to inline all of the CSS rules. This small PHP Class does the whole job for you, saving you lots of time and nerves. Just write your styles in a regular .css file and the PHP library will use the selectors to assign them at the proper tags.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
11
12
13
"><code class="php hljs"><span class="hljs-keyword">use</span> <span class="hljs-title">TijsVerkoyen</span>\<span class="hljs-title">CssToInlineStyles</span>\<span class="hljs-title">CssToInlineStyles</span>;

<span class="hljs-comment">// create instance</span>
<span class="hljs-variable">$cssToInlineStyles</span> = <span class="hljs-keyword">new</span> CssToInlineStyles();

<span class="hljs-variable">$html</span> = file_get_contents(<span class="hljs-keyword">__DIR__</span> . <span class="hljs-string">'/examples/sumo/index.htm'</span>);
<span class="hljs-variable">$css</span> = file_get_contents(<span class="hljs-keyword">__DIR__</span> . <span class="hljs-string">'/examples/sumo/style.css'</span>);

<span class="hljs-comment">// output</span>
<span class="hljs-keyword">echo</span> <span class="hljs-variable">$cssToInlineStyles</span>-&gt;convert(
    <span class="hljs-variable">$html</span>,
    <span class="hljs-variable">$css</span>
);</code></pre>

<hr />

<h3><a href="https://github.com/danielstjules/Stringy" target="_blank">Stringy</a></h3>
Library for doing all kinds of string manipulations. It offers a ton of different methods for modifying text (<code>reverse()</code>, <code>htmlEncode()</code>, <code>toAscii()</code> etc.) or gather information about a string (<code>isAlphanumeric()</code>,<code>getEncoding()</code>, among others). A cool thing about Stringy is that it also works with special symbols like Greek or Nordic letters;
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
11
12
13
"><code class="php hljs">s(<span class="hljs-string">'Camel-Case'</span>)-&gt;camelize(); <span class="hljs-comment">// 'camelCase'</span>

s(<span class="hljs-string">'   Ο     συγγραφέας  '</span>)-&gt;collapseWhitespace(); <span class="hljs-comment">// 'Ο συγγραφέας'</span>

s(<span class="hljs-string">'foo &amp; bar'</span>)-&gt;containsAll([<span class="hljs-string">'foo'</span>, <span class="hljs-string">'bar'</span>]); <span class="hljs-comment">// true</span>

s(<span class="hljs-string">'str contains foo'</span>)-&gt;containsAny([<span class="hljs-string">'foo'</span>, <span class="hljs-string">'bar'</span>]); <span class="hljs-comment">// true</span>

s(<span class="hljs-string">'fòôbàř'</span>)-&gt;endsWith(<span class="hljs-string">'bàř'</span>, <span class="hljs-keyword">true</span>); <span class="hljs-comment">// true</span>

s(<span class="hljs-string">'fòôbàř'</span>)-&gt;getEncoding(); <span class="hljs-comment">// 'UTF-8'</span>

s(<span class="hljs-string">'&amp;amp;'</span>)-&gt;htmlDecode(); <span class="hljs-comment">// '&amp;'</span></code></pre>

<hr />

<h3><a href="https://github.com/consolidation-org/Robo" target="_blank">Robo</a></h3>
Robo is a Gulp-like task runner, only for PHP. With it you can set up automations that improve your workflow and the time it takes to build a project after making changes. Robo can run tests, compile code from preprocessors, handle version control updates, and many other useful tasks.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
"><code class="php hljs"><span class="hljs-comment">// Doing a Git Commit with Robo</span>
<span class="hljs-keyword">public</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">pharPublish</span><span class="hljs-params">()</span>
</span>{
    <span class="hljs-variable">$this</span>-&gt;pharBuild()-&gt;run();
    <span class="hljs-variable">$this</span>-&gt;_rename(<span class="hljs-string">'robo.phar'</span>, <span class="hljs-string">'robo-release.phar'</span>);
    <span class="hljs-keyword">return</span> <span class="hljs-variable">$this</span>-&gt;collectionBuilder()
        -&gt;taskGitStack()
            -&gt;checkout(<span class="hljs-string">'gh-pages'</span>)
        -&gt;taskGitStack()
            -&gt;add(<span class="hljs-string">'robo.phar'</span>)
            -&gt;commit(<span class="hljs-string">'robo.phar published'</span>)
            -&gt;push(<span class="hljs-string">'origin'</span>, <span class="hljs-string">'gh-pages'</span>)
            -&gt;checkout(<span class="hljs-string">'master'</span>)
            -&gt;run();
}</code></pre>

<hr />

<h3><a href="https://github.com/coduo/php-humanizer" target="_blank">PHP Humanizer</a></h3>
This library takes variables and transforms them into a more human-readable format using a set of methods. For example it can turn Roman numerals into numbers, truncate long strings, and calculate bytes to kB/MB/GB. Support for over 15 languages (the spoken kind, not programming ones).
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
11
12
"><code class="php hljs"><span class="hljs-keyword">use</span> <span class="hljs-title">Coduo</span>\<span class="hljs-title">PHPHumanizer</span>\<span class="hljs-title">NumberHumanizer</span>;

<span class="hljs-keyword">echo</span> StringHumanizer::humanize(<span class="hljs-string">'field_name'</span>); <span class="hljs-comment">// "Field Name"</span>

<span class="hljs-keyword">echo</span> NumberHumanizer::ordinalize(<span class="hljs-number">1</span>); <span class="hljs-comment">// "1st"</span>
<span class="hljs-keyword">echo</span> NumberHumanizer::ordinalize(<span class="hljs-number">23</span>); <span class="hljs-comment">// "23rd"</span>

<span class="hljs-keyword">echo</span> NumberHumanizer::toRoman(<span class="hljs-number">5</span>); <span class="hljs-comment">// "V"</span>
<span class="hljs-keyword">echo</span> NumberHumanizer::fromRoman(<span class="hljs-string">"MMMCMXCIX"</span>); <span class="hljs-comment">// 3999</span>

<span class="hljs-keyword">echo</span> NumberHumanizer::binarySuffix(<span class="hljs-number">1024</span>); <span class="hljs-comment">// "1 kB"</span>
<span class="hljs-keyword">echo</span> NumberHumanizer::binarySuffix(<span class="hljs-number">1073741824</span> * <span class="hljs-number">2</span>); <span class="hljs-comment">// "2 GB"</span></code></pre>

<hr />

<h3><a href="https://github.com/thephpleague/color-extractor" target="_blank">ColorExtractor</a></h3>
The last item on our list is this small library for extracting colors from images. It iterates all of the pixels in a given picture and returns a palette of the colors on it sorted by total area. Developers can then use this palette to get the most dominant colors and adapt the design according to them.
<pre class="brush:php" data-lines="1
2
3
4
5
6
7
8
9
10
"><code class="php hljs"><span class="hljs-keyword">require</span> <span class="hljs-string">'vendor/autoload.php'</span>;

<span class="hljs-keyword">use</span> <span class="hljs-title">League</span>\<span class="hljs-title">ColorExtractor</span>\<span class="hljs-title">Color</span>;
<span class="hljs-keyword">use</span> <span class="hljs-title">League</span>\<span class="hljs-title">ColorExtractor</span>\<span class="hljs-title">Palette</span>;

<span class="hljs-variable">$palette</span> = Palette::fromFilename(<span class="hljs-string">'./some/image.png'</span>);

<span class="hljs-variable">$topFive</span> = <span class="hljs-variable">$palette</span>-&gt;getMostUsedColors(<span class="hljs-number">5</span>);
<span class="hljs-variable">$colorCount</span> = count(<span class="hljs-variable">$palette</span>);
<span class="hljs-variable">$blackCount</span> = <span class="hljs-variable">$palette</span>-&gt;getColorCount(Color::fromHexToInt(<span class="hljs-string">'#000000'</span>));</code></pre>
