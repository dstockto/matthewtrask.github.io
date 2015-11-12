---
layout: post
title:  "Let's build a website, pt 1."
date:   2015-11-11
comments: yes
description: With the help of Composer and Bower, Im going to take you on a journey to build a site. 
tags: Composer, AtlantaPHP, PHP, SlimPHP, Packagist, Getting Started
---

##Composing a great website

It's no secret that creating a website has undergone a transition right? First it was basic HTML, CSS, some fun Javascript and there you go. Then, as Jeffery Way says [here](https://youtu.be/mDotS5BDqRM?t=11m6s), its just not those three anymore. Now, as developers, we need a lot of things. Tools like:

* HTML	
* CSS -> Bootstrap/Foundation
* Javascript
* jQuery 
* Angular, Vue, React, Ember or whatever cool framework it is now.

But then we need someway to validate data and parse it on a server so:

* PHP
* Ruby
* Python

How will we save our data? Well we cant just keep it in a session. So

* SQL
* MongoDB

But it doesnt stop there! As Jeffery keeps on going, theres so many tools out there just to build a simple website. So whats needed, and whats not? Well, that is completely up to you! So lets talk about what we are doing. Our project, which Im documenting, is going to be a rebuild of [AtlantaPHP.org](https://atlantaphp.org). 

## What do we need to start?

Well, if you truly want to follow along, you will need the following tools:

* [vagrant](https://vagrantup.com)
* [github](https://github.com)
* [composer](https:getcomposer.org)
* [Scotch Box](https://box.scotch.io)

These 4 tools will be the base of my project. As an aside, there are a few other developers working on this project, but Im leading the project. So once you get Vagrant up, lets build our composer.json file. Take a look!

<pre>
	<code class='javascript' style="font-size: 12px">
	{
		"name": "Atlanta/AtlantaPHP", 
		"description": "PHP User Group for Atlanta, GA. Meets first Thursday of every month at Atlantic Station",
		"type": "Website",
		"license": "MIT",
		"authors": [
			{	
			"name":"Matt Trask", 
			"email": "mjftrask@gmail.com"
			}
		],
		"require": {
			"slim/slim": "^3.0@beta",
			"slim/views": "0.1.3",
			"slim/pdo": "1.8.*", 
			"twig/twig": "1.23.*", 
			"slim/logger": "0.1.*",
			"ircmaxell/password-compat": "1.0.4",
			"phpmailer/phpmailer": "5.2.14",
			"guzzlehttp/guzzle": "6.1.*",
			"nesbot/carbon": "1.14.*",
			"dms/meetup-api-client": "2.0.*"
		},
		"require-dev": {
			"phpunit/phpunit": "4.8.18",
			"phploc/phploc": "*",
			"fzaninotto/faker": "1.5.*",
			"squizlabs/php_codesniffer": "2.3.*"
		}
	}
	</code>
</pre>

So lets break down this file so you know whats going on. And it can be a good intro into Composer. 

Composer first and foremost is a PHP Package Manager. I put in the packages I want, with constrants to the version numbers. If you like at the first require statement, these are all what I want to build the website.I am asking Composer to find and pull in the [Slim](https://slimframework.com) framework at version 3. Now I have to pull it in different cause technically Slim v3 isnt in production yet, but stable enough to use. 

Going back a step, if you look at the file, its all based around JSON Arrays. The top part is just general meta data about the project. Name of the project, who is working on it, how can they be contacted, etc. If this were a package I was publishing, I would be adding keywords as well as requirements like PHP version numbers, so that way people know what is needed for my library to run. Right now, we are just doing that should someone come to the project and want to know who to talk to. Which is me, currently. 

## SemVer

This is a good point to bring up something called Semantic Versioning. If you look at the numbers in my composer.json file, they all follow the pattern of '1.2.3' where each numbered spot has a posiion. 

### 1 means Major

The first place, the 1 in my example, represents a major package. When you hit 1, 2, 3, 4, etc you are releaseing code that in the package that is not backwards compatibilty and will be breaking to versions under it. So if i release Slim 4.x, you shoul expect it will not play well with Slim 3.x, or Slim 2.x
Major releases are usually annouced, and with some fanfare. I see people start a watch for the next Laravel major relase. Its kind of a big deal. 

### 2 means Minor

Minor patches or changes are less violent in terms of API changes. These patches, the x.1.x changes, will allow for backwards compatibility. Usually these types of fixes are features that couldnt be built into the initial 1.x.x release, so the developers bundle it up into a x.1.x release to make sure the feature is going to work the way its expected. 

### 3 means Bugs

Just like is says, a x.x.1 release is just a bug fix. Misspelt a function, or the function is returning n+1, well thats a quick bug fix will not affect the code you are bringing in. These are the most frequent changes you will run into as a developer. 

So anyways, with Composer, we have a few types of options to do. We can hard lock our dependencies:
<pre>
	<code type="javascript">
		"require": {
			"slim/views": "0.1.3"
		}
	</code>
</pre>

which means that no matter how many times I run 

<pre>
	<code type="javascript">
		/var/www/public composer install
	</code>
</pre>

the code for 'Slim/Views' will always return 0.1.3. as the version and codebase I will use to create a templating engine in Slim. 

## Hard Locking can be dangerous

While some apps, and some people, hard lock the composer dependencies, for this project, and the amount of code distribution, we will want to allow for a little variance in the code. If Im writing a project on my own, and I know what I want, I will hard lock the dependencies. But for right now, its ok to allow variance. Generally, I will hard lock to the minor version, just to be safe, but bug fixes can come in randomly. 

Other ways you can pull in code, is with the '^' symbol and '~' symbol. Both are more soft dependency types, allowing for code base fluctuation. 

## Require-Dev

The next, and one the most important parts of the composer.json is whats in the "require-dev" array. If you look, I have:
<pre>
	<code type="javascript">
		"require-dev": {
			"phpunit/phpunit": "4.8.18",
			"phploc/phploc": "*",
			"fzaninotto/faker": "1.5.*",
			"squizlabs/php_codesniffer": "2.3.*"
		}
	</code>
</pre>

These allow me to test my code (phpunit), see the amount of code/methods/classes in the code (phploc), a way to fake data to test my code, (faker) and PHP_codesniffer to lint the PHP I wil write for the project. These libraries are used in the dev stage only, and not to be pushed to the server. But generally these code libraries are invaluable to developers.  

According to Jordi Baggiano, who wrote Composer, require-dev is installed on composer update only, unless explicitely stated on the install command:

<blockquote style="font-size: 14px">
The update command now installs dev requirements by default. This makes sense since you should only run it on dev environments. No more update --dev, the dev flag is now implicit and if you really don't want these packages installed you can use update --no-dev instead.


The install command on the other hand remains the same. It does not install dev dependencies by default, and it will actually remove them if they were previously installed and you run it without --dev. Again this makes sense since in production you should only run install to get the last verified state (stored in composer.lock) of your dependencies installed. 
</blockquote>

## Now what?

Well, once you run "composer install", it will pull in all the code of the composer file, and set up the libraries in the callable 'vendor' directory. From there we can use the specific libraries for the methods we need them for. 

Before you run composer install, you wont have a Vendor directory. Then you should run composer update to get the require-dev packages. Afterwards, it will appear. If you open it up, you will see a lot of separate folders with packages that you have now pulled in. Open them up and explore a bit! We will start with bringing in SlimPHP to our project. That will come next time!


## Next time. 
Part 2 will explore building a base Slim PHP project. We will talk briefly on Slim, Twig, a little more composer stuff, such as the lock file, and how to distribute code via Github to a team. We will also look at NPM and Bower.io for front end package management as well. Stay Tuned! 




