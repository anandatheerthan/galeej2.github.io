---
layout: post
title: Blade :: Extend
date: 2016-01-27 15:00
author: administrator
comments: true
categories: [Laravel]
---
1) create <code>app/Providers/BladeServiceProvider.php</code>
<pre class="lang:php decode:true ">&lt;?php namespace App\Providers;

use Illuminate\Support\ServiceProvider;

class BladeServiceProvider extends ServiceProvider
{
    public function boot()
    {
        /* @datetime($var) */
        \Blade::extend(function($view, $compiler)
        {
            $pattern = $compiler-&gt;createOpenMatcher('datetime');

            return preg_replace($pattern, '$1&lt;?php echo $2-&gt;format(\'m/d/Y H:i\')); ?&gt;', $view);
        });

        /* @eval($var++) */
        \Blade::extend(function($view)
        {
            return preg_replace('/\@eval\((.+)\)/', '&lt;?php ${1}; ?&gt;', $view);
        });
    }

    public function register()
    {
        //
    }
}</pre>
&nbsp;

2) in <code>config/app.php</code> add
<pre class="lang:php decode:true ">&lt;?php

return [

    // ...

    'providers' =&gt; [

        // ...

        'App\Providers\BladeServiceProvider',</pre>
&nbsp;

3) run <code>php artisan clear-compiled</code>

4) in your template use <code>@datetime($updated_at)</code> or <code>@eval($var = 1)</code>, <code>@eval($var++)</code> for example

5) important remark
<blockquote><code>blade</code> templates are cached, try to make a dummy change in blade, this way laravel will recompile the template</blockquote>
