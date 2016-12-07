---
layout: post
title: Laravel 5.3 is now released
date: 2016-08-26 14:26
author: administrator
comments: true
categories: [Laravel]
---
The Laravel team is proud to announce the <a href="https://laravel.com/docs/5.3">release</a> of Laravel 5.3 and it’s now available for everyone. The new features in 5.3 are focused on improving developer speed by adding additional out of the box improvements for common tasks.

This is a general release and comes with six months of bug fixes and security fixes are provided for one year. <a href="https://laravel-news.com/2015/06/laravel-5-1-released/">Laravel 5.1</a> is the latest LTS release which includes bug fixes for two years and security fixes for three years.

Here is a quick overview of some of the highlights of the new 5.3 release:
<h2>New Home Page</h2>
<img class="aligncenter size-large wp-image-7058" src="https://d1zj60nuin5mrx.cloudfront.net/media/2016/08/23093612/laravel-homepage-1200x991.png" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 1362px) 62vw, 840px" srcset="https://d1zj60nuin5mrx.cloudfront.net/media/2016/08/23093612/laravel-homepage-1200x991.png 1200w, https://d1zj60nuin5mrx.cloudfront.net/media/2016/08/23093612/laravel-homepage-600x495.png 600w, https://d1zj60nuin5mrx.cloudfront.net/media/2016/08/23093612/laravel-homepage-768x634.png 768w" alt="laravel-homepage" width="840" height="694" />

The <a href="https://laravel.com/">home page</a> received a makeover with boxes showcasing the new packages, and more community resources including links to Laracast, Laravel News, and Statamic.
<h2>Laravel Scout</h2>
Laravel Scout is a new driver based full-text search engine for Eloquent. Scout works by adding a new <code>Searchable</code> trait to your models, syncing your data to the index of choice, and then you can search as easily as:
<pre><code class="hljs php">Post::search(<span class="hljs-string">'Alice'</span>)-&gt;get();
</code></pre>
<h2>Laravel Passport</h2>
<a href="https://laravel-news.com/2016/08/laravel-passport/">Laravel Passport</a> is designed to give you everything you need to deploy your own OAuth2 server in a matter of minutes. It’s an optional package that comes complete with the ability to set your scopes, Vue.js components for token generation, revoking tokens, and more.
<h2>Laravel Mailable and Notifications</h2>
<a href="https://laravel-news.com/2016/08/laravel-mailable-the-new-and-improved-way-to-send-email-in-laravel/">Laravel Mailable</a> is a new class-based approach to sending emails that will allow you to simplify sending email by removing the need for the closure style.

<a href="https://laravel-news.com/2016/08/laravel-notifications-easily-send-quick-updates-through-slack-sms-email-and-more/">Laravel Notifications</a> allow you to send out quick updates through services like Slack, Text messages, Email, and more. The community has even started a “<a href="http://laravel-notification-channels.com/">Laravel Notifications Channel</a>” group where anyone can submit drivers and it already includes over twenty-six drivers.
<h2>Laravel Echo</h2>
Laravel Echo is an improvement to the existing event broadcasting system that makes it easy to work with web sockets. To utilize Echo the backend will ship with the Laravel core and then you will need to pull in an NPM package for the JavaScript side.
<h2>Migrations</h2>
The migrations system received a new feature that will allow you to rollback a single migration.
<pre><code class="hljs">php artisan migrate:rollback --step=1
</code></pre>
Previously, this option did not exist and you could only rollback a single batch, which could contain multiple steps.
<h2>Simple Pagination</h2>
Laravel offers two styles of pagination. An advanced style that shows a list of page numbers and a simple style that only show a previous and next link.

Starting with this release the simple pagination will now be available from a view file which makes it easier than ever to customize to your sites design and HTML structure.
<h2>Blade Loop Variable</h2>
Laravel Blade received a new <code>$loop</code> variable that will give you finer grain control within your loops. Now you can use the following properties:
<ul>
 	<li>index – The number of the loop.</li>
 	<li>remaining – How many loops remain</li>
 	<li>count – The total count</li>
 	<li>first – If it’s the first loop</li>
 	<li>last – If it’s the last</li>
 	<li>depth – How many levels deep you are.</li>
 	<li>parent – Allows you to call the parent in a nested loop.</li>
</ul>
For more on this see <a href="https://mattstauffer.co/blog/the-new-loop-variable-in-laravel-5-3">Matt Stauffer’s</a> blog post.
<h2>Directory Changes</h2>
The “app” folder was simplified by removing all the empty folders like Events, Jobs, Listeners, and Policies. This remains fully backward compatible and if you run any Artisan “make:” command related to these features the folder will get added back.
<h2>Queued Jobs</h2>
Eloquent Collections are now cleanly serialized and re-pulled by queued jobs the same way individual models are.

This is beneficial in the cases where the data in the Eloquent Collection has changed since the job was pushed onto the queue.
<h2>Query Builder</h2>
The query builder will now return a Collection by default instead of an array. This is potentially a breaking change but it will now keep results from either the query builder or Eloquent uniform.
<h2>Cache Helper</h2>
Laravel 5.3 includes a new <code>cache()</code> global helper that allows you to <code>get</code>, <code>put</code>, or<code>return</code> an instance of the backing service. For more information check out <a href="https://mattstauffer.co/blog/the-new-cache-global-helper-in-laravel-5-3">Matt’s</a>post on this.
<h2>Documentation Changes</h2>
The documentation received a huge overhaul for this release. It’s now divided into better sections that guides you from installation all the way through Laravel’s official packages. It is also linking to relevant free Laracasts videos on certain topics. This will cater to either people that prefer audio/video for learning and those that enjoy reading.
<h2>Upgrade Guide</h2>
The official documentation has the <a href="https://laravel.com/docs/master/upgrade">upgrade guide</a> which includes all the information you need to start using 5.3 today. It estimates the total time of upgrading at two to three hours.
