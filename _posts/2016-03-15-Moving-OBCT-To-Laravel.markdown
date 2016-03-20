---
layout: post
title:  "Moving OBCT to Laravel"
date:   2016-03-15
comments: yes
description: After Lets Encrypt blew up the site, I decided it was a good time to make some changes    
tags: Laravel, Dev, PHP
---

# Laravel New OBCT

I have this project. It's not glamorous, its not a super profitable website, but it is one I enjoy working on. We developers tend to
have one or two that are close to our hearts. No matter how frustrating it can be, you put this project first and make it happen.
For me, its [OBCT](http://offbroadwaykids.net). I taught guitar lessons there for a few years, and it was an absolutely wonderful
place to be. The owners, Shannon and Chris, have done a great job fostering an amazing community there. Kids are able to come learn
the art of dancing and music in a fun environment.

Well, when I moved to programming, they asked if I could update their site. Of course! Without going into too many details, the code
for this site resembles my career. First it was a mess, includes and requires everywhere. Then I learned the joys of frameworks. So I
moved the site to a framework. That wasn't enough, as I learned about setting up my own servers. Tons of trials and errors. But now,
we are at the point of this past week.

## Use Lets Encrypt they said.

Its making the rounds now. Its an open source library that lets you place SSL, or Secure Socket Layer, certificates on your web server.
If you dont know what it is, go visit a site, and click on the url at the top. You'll see a locked symbol and hovering over it should
reveal details about the SSL cert. Everyone was raving about it, so why not? An SSL is a great thing, it protects all web traffic data.
And with some of the ideas I was coming up with for OBCT, an SSL was needed. (Sidenote, I tend to treat OBCT as a playground. I bring
libraries in here and use them so I can see if I like them or not).

This past week I got a notice to update the cert. No biggie, I look and the command is something like

```command-line
  ./lets-encrypt renew
```

so I run it. It gives me the all good and I continue on with my day.  Soon after, I receieved an email saying all the links on the site
were down. This seeming odd, I logged in both SSH'd to the server, and to the site. Sure enough, everything was a 404 error of awesome.
At this point, I tried to undo the Let's Encrypt process, but that was too late. Thinking fast, I knew it was time to blew things up and
start fresh. So I pulled the site down, and destroyed the server.

## Laravel new Obct

So lets look at a few things behind the scenes before I get into more details with the move. Originally the site was built on a framework called [SimpleMVC](http://simplemvcframework.com). I, along with my friend and coworker Justin, had built [Transparent Trade Coffee](http://transparenttradecoffee.com) on the same platform. As the name implies, its dead simple. However, when they released 2.2, they introduced both new packages and breaking changes. If you know anything about SemVer, a X.1.X change should not be breaking. It can introduce new features, but should not break backwards compatibility. But I digress. Other then the framework, there wasnt much else to the site. I had a few packages, mainly Nesbot\Carbon for better time functions. I had the Foundation CSS framework in place.

Deciding to move frameworks is no small feat. And it was even harder when I was giving up my weekend. So Friday night, I ran the inital command and just started. Note that I had some beer. Was worth it. Laravel makes this easy too. With the artisan commands, I was up and running in moments. Starting first with

```command-line
$ php artisan make:migration create_table
```

I had an easy way to start the data migration. I could have used a simple SQL import, but with these commands at my use, I figured I would give this a go. After the date was moved into the tables, all I needed was controllers. With Laravel, there is two options, either you can create your own controllers, or Laravel can build you an awesome HTTP Controller. What that means is that the controller will have specific functions mapped to the verbs of HTTP: Get, Post, Put, Delete, Patch. For this project, I went with custom controllers. Keeping with SOLID, life just got even easier. A mistake I made on the old version was that there was one controller for the whole project. For this project, theres already 10 controllers, and I plan on adding more.

##  Auth

The nice thing about Laravel, is that it is pre-packaged with an auth class, which makes users and passwords that much easier. I plan on writing a post specifically about that in the future. I have found the documentation for it wasnt great. But the idea with OBCT is two things, move the studio off its current platform of class sign ups, and allow people to buy tickets through the site. With the authc classes, these tasks will be insanely easy to accomplish. I already know I need to bring in the Leagues OmniPay package, as well as Fractal. Both these will help make these things happen.

## Thoughts

I have always been weary of Laravel. Multiple times I started a project and got roadblocked fast. So why was it so easy this time? It is cause over the past few months, work has had me focused on POPO, or Plain Old PHP Objects. Using those, without the crutch of a library or framework made spinning up a Laravel application ten times easier. Now I have another tool in the library I can pull out and use.  
