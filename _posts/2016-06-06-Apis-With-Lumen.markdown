---
layout: post
title:  "Speaking at Upstate PHP"
date:   2016-05-23
comments: yes
description: After talking about API's and reading about them, I wanted to build one from scratch and talk about it some more.
tags: Lumen, API, development
---

## APIs and You

Ever since I started writing code, API's have always seemed to be this mystic source of data. When I first started, an API to me was the 
ultimate in programming. Connect it up and get it working with your app? Magic! But as I kept going, the magic and mysticism of it wore off
to just another tool in the tool box. API's are powerful and a lot of fun to use. But there are a lot of bad/not maintained API's out there. 
Unfortunately there are API's that are for bigger companies that tend to be older, and the code standards are just not there. But enough about those, 
what about building your own api? Lets give it a try!

## Tools

Lets keep it simple, and use [Lumen](https://lumen.laravel.com). Its a micro framework from Laravel that is perfect for this type of work.
Install with composer like so 
```
composer create-project --prefer-dist laravel/lumen
```
