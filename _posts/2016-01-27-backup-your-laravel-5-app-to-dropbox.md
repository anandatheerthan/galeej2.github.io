---
layout: post
title: Backup your Laravel 5.1 App to Dropbox
date: 2016-01-27 14:21
author: administrator
comments: true
categories: [Laravel]
---
Packages used
<ul>
	<li><a href="https://github.com/spatie/laravel-backup" target="_blank">spatie/laravel-backup</a> – Backups your filesystem and database to any <a href="http://laravel.com/docs/5.1/filesystem" target="_blank">Laravel file system</a></li>
	<li><a href="https://github.com/thephpleague/flysystem-dropbox" target="_blank">thephpleague/flysystem-dropbox</a> – Adds dropbox as a <a href="http://laravel.com/docs/5.1/filesystem" target="_blank">laravel file system</a></li>
</ul>
<h3>Step 1</h3>
Follow the steps to install <a href="https://github.com/spatie/laravel-backup" target="_blank">spatie/laravel-backup</a> and <a href="https://github.com/thephpleague/flysystem-dropbox" target="_blank">thephpleague/flysystem-dropbox</a>
<h3>Step 2</h3>
Create a file name <strong>DropboxFilesystemServiceProvider.php</strong> in <strong>app/Providers/. </strong>Then add  <strong>App\Providers\DropboxFilesystemServiceProvider::class</strong> to your providers in config/app.php

Below is a copy of my <strong>DropboxFilesystemServiceProvider.php</strong>. Take a look at  <strong>$config[‘accessToken’]</strong> and <strong>$config[‘appSecret’]</strong>. You’ll get these when you create a dropbox app.
<pre>&lt;?php

namespace App\Providers;

use Storage;
use League\Flysystem\Filesystem;
use Dropbox\Client as DropboxClient;
use League\Flysystem\Dropbox\DropboxAdapter;
use Illuminate\Support\ServiceProvider;

class DropboxFilesystemServiceProvider extends ServiceProvider
{
    public function boot()
    {
        Storage::extend('dropbox', function ($app, $config) {
            $client = new DropboxClient($config['accessToken'], $config['appSecret']);

            return new Filesystem(new DropboxAdapter($client));
        });
    }

    public function register()
    {
        //
    }
}
</pre>
<h3>Step 3</h3>
Create a <a href="https://www.dropbox.com/developers/apps/create" target="_blank">Dropbox API App</a>

Make sure you generate an access token. Generating an access token will create a folder Apps in your Dropbox folder. This is where your backups will be saved.
<h3>Step 4</h3>
Edit <strong>config/laravel-backup.php</strong> and set <strong>‘filesystem’ =&gt; [‘dropbox’]</strong>. If you do not have a <strong>laravel-backup.php</strong> file in your config folder, run <strong>php artisan vendor:publish –provider=”Spatie\Backup\BackupServiceProvider”</strong>
<h3>Step 5</h3>
Add a dropbox filesystem to <strong>config/filesystems.php</strong>
<pre>'dropbox' =&gt; [
 'driver' =&gt; 'dropbox',
 'accessToken' =&gt; env('DROPBOX_ACCESS_TOKEN'),
 'appSecret' =&gt; env('DROPBOX_APP_SECRET'),
 ]
</pre>
<h3>Step 6</h3>
Edit <strong>kernel.php</strong> in <strong>app Console/</strong>. This will run your backup and clean up old backups. You can define how many backups you save in <strong>config/laravel-backup.php</strong>. Below is a copy of my <strong>kernel.php</strong>.
<pre>&lt;?php

namespace App\Console;

use Illuminate\Console\Scheduling\Schedule;
use Illuminate\Foundation\Console\Kernel as ConsoleKernel;

class Kernel extends ConsoleKernel
{
 /**
 * The Artisan commands provided by your application.
 *
 * @var array
 */
 protected $commands = [
 'App\Console\Commands\Inspire',
 ];

 /**
 * Define the application's command schedule.
 *
 * @param \Illuminate\Console\Scheduling\Schedule $schedule
 */
 protected function schedule(Schedule $schedule)
 {
   $schedule-&gt;command('backup:clean')-&gt;daily();
   $schedule-&gt;command('backup:run')-&gt;daily();
 }
}</pre>
<h3>Step 7</h3>
Setup scheduler to run your backup. You can do this from a cron job or if you’re using <a href="https://forge.laravel.com/" target="_blank">Forge</a>, you can set it up there. More documentation <a href="http://laravel.com/docs/5.1/scheduling#introduction" target="_blank">here</a>.
