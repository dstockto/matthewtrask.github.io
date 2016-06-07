---
layout: post
title:  "Building an API with Lumen"
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
Install with composer like so: 
```
composer create-project --prefer-dist laravel/lumen api-demo
```

After Composer does its magic, you will be good to go! To make it easier, Im going to put it on a Vagrant box to make development easier for me. Once you get it all set up, lets copy the .env.example to .env. If you are unfamiliar with this file, it contains the connection details for your database. Right now its MySQL, but it can handle Postgres, SQLite, and MSSQL. 

Also included with Lumen comes PHPUnit. But we may need a few other tools. Lets add the following packages:
* league/fractal
* fzaninotto/faker 
* behat/behat
* ramsey/uuid
* 
Why? Well, Fractal helps handle JSON responses, Ramsey/UUID to help hide our user base (more later), Faker to give us fake data to play with and Behat for DDD. But now we are good to get going!

## What kind of API?

Lets just create something simple. A user base would be good and simple. Lets design the database first. We need: first name, last name, age, zip code, email, and uuid. I will post the repo link so you can see the migration. But its going to be a basic table.

// to be continued. 
