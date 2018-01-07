---
layout: post
title:  "Laravel packages I prefer"
date:   2018-01-01
comments: yes
description: A collection of packages I use when I spin up a new Laravel project.
tags: PHP, Laravel, Open Source, Packages
---

## Composer Require 

Ive been spinning up a few new Laravel projects lately, and in my efforts to blog more, figured a good post would be a collection of packages I use when I spin up the new project. [Matt Stauffer](https://mattstauffer.com/blog/what-packages-do-you-install-on-every-laravel-application-you-create/) did a similar post, but he polled Twitter; while this will be just what I prefer to use. 

I will mention a few Javascript packages as well, since I use Vue.js with Laravel almost exclusively now. 

### PHP

* [Laravel Homestead](https://github.com/laravel/homestead)

This is usually number one for me, because right out of the box it just works. There are plenty of other options out there: Laradock, Laravel Valet, custom Vagrant boxes, and more. To me though, Laravel Homestead gets the job done for me. I only have to do one thing when I bring it in and that is adding Xdebug.

* [Laravel Fractal](https://github.com/spatie/laravel-fractal)

A laravel specific wrapper around the the League's Fractal package, this helps create fluent JSON for API responses. It is a fun little library to use requires minimal setup and has a huge benefit to it. Laravel 5.5 has implemented something natively now, but I still prefer to use the Fractal library cause of muscle memory.

* [Laravel Passport](https://github.com/laravel/passport)

Moving from an MVC framework to SPA required me to figure out a new authentication solution and Passport is it. Passport offers a few different solutions out of the box, from OAuth tokens I can generate for other applications to use with mine, or personal access tokens which help with the login flow. Other solutions include Okta, Sentinel and writing your own with the League's OAuth2 Server (nope!)

* [Laravel Socialite](https://github.com/laravel/socialite)

This one is so much fun, and makes it fun to develop with. Socialite takes care of Social Authentication and offers Facebook, Linkedin, Google, Twitter, Github and a few others all with essentially the same interface (Twitter being different because they use OAuth 1 while the rest use OAuth 2). On a project I am collaborating on with [Brian Retterer](https://twitter.com/bretterer) we are debating just using Socialite for our user login, and I can tell you it will be more fun because of Socialite. 

* [League Commonmark](https://commonmark.thephpleague.com)

This is a lovely package written by a good friend of mine [Colin O'Dell](https://twitter.com/colinodell) which allows a user to write Markdown in an application rather then rely on WYSIWYG editors. It usually requires all of 4 or 5 lines of code to get Commonmark up and running and then I get to give users the happiness of using something a lot of us are familiar with.

### Javascript

* [Vue Router](https://github.com/vuejs/vue-router)

Rather than rely on Laravel to do all of my routing, I bring in VueRouter for my front end template routing, and its nice to work with this package. The docs are fantastic, and I can get a router done in under an hour at this point. It can handle things like auth checks as well, which makes it easy to protect routes. 

* [Tailwind CSS](https://tailwindcss.com)

The new component utility library from Adam Wathan, Steve Schoger and a few others has made an impact on the Laravel community. It has a unique style to it, but it is flexible to let me impose my own design ideas (spoiler alert: I don't have any design ideas). I am using Tailwind on the project I mentioned above with Brian, and its been tough moving from Bootstrap, but overall its worth the effort.

There are a few packages I enjoy! Any others I should be checking out?

