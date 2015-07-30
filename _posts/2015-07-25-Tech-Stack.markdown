---
layout: post
title:  "Tech Stack"
date:   2015-07-25
comments: yes
description: What I use to make a website or app happen, from start to finish.
tags: PHP, Tools, Beginnings, APIs, frameworks
---

#How I build apps and sites

I work at LAMP Camp, and since most of the people there are learning, one question I get alot
is what tools do I use? And its an interesting question, because as of late, Ive been changing
my mind and wondering what could be the best way to use the tools I use. Anyways, here is a run
down. Keep an eye on this, cause I will be changing the post as I mess around with new tools. Lets
treat this as if I just bought a new machine, and I want to set it up for development.

##Machine
First and foremost, I am a Mac guy. I dont live and die with every decision they make, but
they make good computers. Its a 2011 Macbook Pro, with 16 gigs or ram and 120 gig SSD. The SSD was
the best decision I have made. Super fast, it sped my computer up and helped my workflow. Lately, however,
Im not overly thrilled that Apple is soldering the ram and hard drives into the machine. Purely a business
move to get more revenue, but still sucks. One trick I do like to do is remove the programs from the dock.
It helps me keep track of what is open, and keeps the dock small and less distracting.

Now, I do have a Linux machine too, running a distro called ElementaryOS. They got some flack for
trying to charge for their distro, and while I cant blame them for trying to make a living, it was
kind of a dick move.

##Computer Programs
Theres a few Mac specific programs I use to really optimize how I work. First thing I get is
[Homebrew](http://brew.sh/). It's *the* package manager for a Mac. To browse packages, check out this [page](http://braumeister.org/). As you can see, theres Apache, Python, PHP, and others that you may want or need.

After I set up Homebrew, I get a version of [iTerm](iterm2.com). It has a ton of awesome features that help speed
things up for me. As a PHP developer, I spend a lot of time in the command line, and iTerm has some features I can't live
without anymore. Split screen is fantastic, and I hot key it on the '~' key. To aid in the terminal, and to make it a little
less bland, I grab a copy of [Oh My Zsh](http://ohmyz.sh/). It has a ton of plugins you can call upon, and it the color scheme
helps keep it from getting dull after hours of looking at the terminal. Truly a godsend in my opinion.

Anpther app that is awesome is [Dash](https://kapeli.com/dash). Dash allows me to download any language's api documents and read them offline. When I took a trip to Maui a few months ago, I used it to code some PHP while in the air without Wifi. Sidenote, its an 8 hour flight, thats a cash cow in terms of internet usage fees. Why cant American Airlines offer wifi on the flights to Maui?!

The last thing I get specific to the Mac, is [Sequel Pro](http://www.sequelpro.com/). Have you ever worked with command line MySQL or even worse, PHPMyAdmin. Yea, this solves the headaches. Its clean, fast, easy to use, allows for SSH tunnels for connections and an easy way to export tables to keep work up to date.

Outside of these, I get Pomodoro Time from the app store, Evernote for note taking, Spotify for music.

##Development Specific Tools
As a PHP Developer, there are a few awesome things that I need in order to maximize my workflow.

First, is a text editor. And for that, its hard to beat [Atom](atom.io). Its my favorite word, free, and very customizable. I'll download it, and then get plugin support for Twig and LinterPHP for all of the linting tools out there. PHP Codesniffer is awesome to use, I highly recommend it. Clean code is good code. You can also get a plugin that will let you see PHPUnit test results in the text editor.

If you are looking for something more powerful, its hard not to recomment [PHPStorm](jetbrains.com). The license may seem steep, but honestly, everything that it offers is unrivaled. PHPUnit support, Vagrant support, Git support, code completion and error checking just to name a few. I absolutely love it. But I only try to use it when Im plugged into power cause it can cause your battery to die off quickly.

##Local Development
For local development, it is hard to beat [vagrant](http://vagrantup.com). Vagrant, along with [VirtualBox](virtualbox.org) make for a great team. Vagrant allows quick access to virtual machines. Super helpful if you are working on a distributed team and need to have everyone on the same server enviornment, or want to have some fun learning Linux without blowing up a computer. Vagrant allows you to configure the VM as you want. If you want CentOS, MySQL, Ruby, PHP, and Node then you just add it to a bootstrap.sh file and once you build your vagrantfile, you run the shell file and it will install everything. There are already a lot of pre-made boxes out there, but making it yourself wouldn't hurt at all. We use Vagrant at work and I use it at home. I cant tell you how awesome it is. Doesnt require the internet either. I put EVERYTHING on my vagrant instance. Git, Composer, Node and all my files. No more cluttering up my computer with tons of unneeded files. Instead, this keeps it nice and neat. I pass the vagrantfile to Github as well, so if someone wants to do a pull request, they have the enviornment I am using as well. Makes checking pull requests so much easier. 

##Front End
If Composer makes back end package management easy, NPM and Bower make Front End that much easier too. If I want Bootstrap, Bower install bootstrap, if I want Gulp (hell yea I do!), then npm install gulp and everything else I need related to Gulp. It makes life so much easier. I can spin up a project in an instant with Bower and Composer, rather then hunting around for 8 different website repos to get the code I want to make my projects. 

Comments or questions?


