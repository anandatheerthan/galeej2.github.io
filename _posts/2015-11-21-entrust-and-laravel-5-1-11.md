---
layout: post
title: Entrust and Laravel 5.1.11
date: 2015-11-21 11:55
author: administrator
comments: true
categories: [Laravel]
---
Entrust is an great Authentication System with Roles and Permission features but Laravel has introduced ACL in 5.1.11 version using Gates. If you have or want to use Entrust, you need to make following changes or else you will end up facing "Method can defined in trait" error.
<pre class="lang:default decode:true ">// ...
class User extends Model implements AuthenticatableContract,
                                    AuthorizableContract,
                                    CanResetPasswordContract
{
    use Authenticatable, Authorizable, CanResetPassword;
    // ...
with the following:

// ...
use Zizaco\Entrust\Traits\EntrustUserTrait;

class User extends Model implements AuthenticatableContract, CanResetPasswordContract
{
    use Authenticatable;
    use CanResetPassword;
    use EntrustUserTrait;
    // ...</pre>
&nbsp;
