---
layout: post
title:  "Why won't people teach PHP?"
date:   2018-10-27
comments: yes
description: PHP has long been known as a language to start on and then quickly move away from. But with a robust ecosystem, solid OOP and more, is it time for that to change?
---

Learn to code! Everyone should learn how to write code they say. The future is going to be dominated by the machines and we will need to control them. Not really, but its true automation is coming and people are going to be coded out of jobs at some point. Because of this we have seen the rise of the coding school generation... the group of people who paid an average of $11,906 [1](https://www.coursereport.com/blog/coding-bootcamp-cost-comparison-full-stack-immersives) to spend anywhere from "Immersive boot camps usually last 2 months to 7 months" [2](https://www.coursereport.com/coding-bootcamp-ultimate-guide) learning how to write web applications in the dreams of making a solid career for themselves. It's not a folly, plenty of people have done it. But, a look at code boot camps around shows that PHP is not a language taught regardless of the demand. This needs to change. 

### 14k jobs on indeed.com along

That number above comes from the website CodingDojo [3](https://www.codingdojo.com/blog/7-most-in-demand-programming-languages-of-2018/) where they analyze job openings on Indeed.com (not linking them). Now, I have never ever looked for a job on Indeed. I will admit I am _very_ fortunate for that. I have been lucky enough that I have cultivated an awesome network of people who have paid attention to me (That Ewok quota won't fill itself). However, there is a whole group of programmers who exist in the world who don't do community on my level. For them, Indeed.com is a place to check out jobs, salary ranges and things like that. So we are currently at a hole of 14k jobs. [Larajobs](https://larajobs.com) specializes in Laravel development jobs usually has around 50 or so posts alone. So why is PHP not being taught? There is demand. So we can rule out a lack of demand. And to be quite clear, this is one website. I didn't bother to look at Monster, Career Builder, AuthenticJobs, WeWorkRemotely, and so many more. I also didn't just do what I normally do which is to post on Twitter, get a ton of retweets and 7 or 8 people hitting me up about opportunities they know of internally.

### Tech Problems?

One thing that could be a cause is that PHP needs a server in order to run the interpreter. Well, so does Ruby and Python. One local boot camp is teaching .NET. I can't imagine the pain it is to get that working on Mac or Linux but they do it (I have not tried to get .NET up and running on my Mac so this could be off base). I just googled "How to run ruby locally" and it looks like you can `gem install` your way to a working application, but if the code school isn't enforcing strict OS requirements for their students then this becomes a pain point. Same thing with Python. And which Python should you teach, 2 or 3? Python 2 has an EOL date of [2020](https://hg.python.org/peps/rev/76d43e52d978) so which do you teach? As we have seen with PHP, "security be damned" and people stick on the version they are comfy with. If you don't believe me look at [http://phpversions.info](http://phpversions.info) and see how many hosts are offering EOL'd versions of PHP as a default! 

Back to the tech problem with PHP, yes you need a server but with tools like Vagrant (used in so many shops around the country), you could solidify a dev environment for everyone as well as introduce a new tool into their developer toolkit for them to show off. It's a win-win. I understand why Javascript is so heavily offered. It requires nothing. You can easily open the dev tools, type `alert('Yub Nub!');` and you have effectively written a line of code without altering the state of your local machine. Pretty cool I will see. Javascript isn't the answer to everything though, it's definitely not the answer to life (that is 42, duh), but it has many many uses. You could teach Javascript and PHP in concert with each other. These are two _very_ similar languages and creates stronger graduates coming out of the boot camp.

### The Junior Problem?

As I theorized on Twitter for this article, one thing I initially didn't take into account is arguably the biggest problem facing developers right now... the lack of real mentorship and chance taking. It's no secret that code camps, at a certain level, will accept anyone cause they need the money and funding to keep going. This creates a strain on the instructors and a strain on employers. The old adage rings true here "Fool me once, shame on you. Fool me twice, shame on me" in that no employer wants to be burned once, let alone twice, for a bad hire. It looks bad up and down the org chain if you hire someone and have to let them go for performance reasons after you thought they would be great. Now it happens to us all, I understand, but managers can't take this risk time and time again. This proves to be a problem and one we are seeing personally pop up in Nashville. I'm not going to name and shame, but there is one coding school who keep pumping out graduates even after the community has outwardly said: "hold the fuck up and calm down". These are full classes of 20 plus soon to be programmers and there are multiple ones. The instructors are strained and can't provide the mentoring needed so they turn to former students of the school. Why they won't open it to the whole community is beyond me, but they bring in past students who are now full-time developers to help. This is a nasty cycle of burn out waiting to happen. As much as I love to code and build things, sometimes you need to not be at a computer. 

So as they take in full cohorts of students and graduating them all into an oversaturated market, many have trouble finding jobs because there is a true burn out sensation taking place in companies. Not every company can handle hiring raw junior developers. They need mentoring, hand holding, and so much more. Believe me, we were all there. Unfortunately, a lot of jobs are trial by fire or pushing the developer in the deep end without sweet looking floaties. The blame is on both the employer and the code school but unfortunately, the one that suffers is the graduate looking for a job. But as technology rapidly advances (I'm sure a new Javascript framework was released in the time I wrote this), juniors are under more pressure to learn the latest and greatest rather than the programming fundamentals crucial to career longevity. 

Can code schools do better? Absolutely. Can employers do better? Absolutely. But that asks two things: it asks the boot camp to reset, and lower their profits in exchange for smaller classes and more developer support and it asks for employers to be more supportive, take time and understand that juniors can absolutely perform at a good level as long as they are given the help they need. Unfortunately, I think this is a mindset change that needs to occur cause I believe that this is something employers think code schools should be doing and vice versa.

There are movements out there to try and fix this. In PHP, we used to have PHP Mentoring, but its since died an uneventful death of lack of interest, burn out, and lack of promotion. Sounds like the cycle of FOSS. April Wensel goes around the country talking about "Compassionate Coding" and trying to get people to realize being nice and empathetic instead of pushing someone in the deep end (YOLO) is a way to promote junior developer growth, more stable organizations and more. Is it working? I think so but give it a few more years first. 

### Build cool shit with boring technology

Back to the PHP problem we face, which is the why of it all. Why won't you teach PHP? Common answers include preconceived notions that are born out of lurking on the internet instead of actually writing a line of PHP, the fact that the PHP ecosystem isn't burning down the world like Javascript is (seriously, I like things they way they are... stable releases and boring technology) and more. 

For the first part, we can talk about that in a bit, cause its a _huge_ thing to tackle. The second, though, isn't. I quipped the other day in a local slack when a developer made a comment about PHP being ugly with the `$` in front of all variables to which I replied, "that's just my reminder my bank account is full and I can do fun shit". This is a common trope pushed around about PHP. Then a few developers pop out of the woodwork to say they worked with PHP once, and it's either "never again" or "it wasn't bad" The root cause of this is before PHP version 5.3, PHP was a procedural language with no support for Object-Oriented Programming, which is a paradigm programmers going through comp sci learn so for them to pick up a procedural language isn't ideal. I get that, I really do. However, as of the current writing of this blog post, we are on 7.2, weeks away from 7.3 and the language is buzzing with excitement around what has happened in the last few years. We have seen PHP get a massive speed increase, support for OOP, adoption of Libsodium into the core for some of the best cryptography and security out there. Just a few weeks ago, an RFC (request for comments) was passed giving PHP the ability to have typed properties. Instead of

```php
/** @var UserIdentity */
private $userIdentity;

public function __construct(UserIdentity $userIdentity)
{
    $this->userIdentity = $userIdentity;
}

public function getUserIdentity() : UserIdentity
{
    return $this->userIdentity;
}

public function setUserIdentity(User $user) : void
{
    $this->userIdentity = $user;
}
```

we can now use something cleaner: 

```php

private UserIdentity $userIdentity;

public function __construct(UserIdentity $userIdentity)
{
    $this->userIdentity = $userIdentity;
}
```

This is on top of scalar type hinting and return type hinting for more robust type safety. But this isn't cool enough apparently! We don't have a framework coming out every week. We do have framework flamewars at times (Symfony v Laravel amirite?) but that's nothing. We have a package manager that doesn't shit the bed, we have a strong OSS community, great conference speaker community, and a wonderful user group community. The support for PHP is there from the community. 

Even with all of this though, PHP isn't considered cool or profitable for companies and boot camps. Which makes me laugh because at my company, at the peak of our busy season we handle millions of requests on PHP 7.2 with Symfony 4, Doctrine, MySQL, MongoDB and a few other tools with jQuery and Backbone on the front end. We do continuous deployment and we deploy without fear (well others do. I'm still terrified I'll take production down) throughout the day. Even on Friday afternoons, we deploy. We have thousands, THOUSANDS of unit and feature tests. And it's boring af. I don't mean the job, I like the job, and I like the people I work with. But the code is boring. We aren't flashy, we aren't hipsters, we just focus on clean code and thorough reviews (you should see some of my PRs). But handling millions of requests on boring technology isn't cool to teach. 

### A world of teaching PHP

That was a lot of typing for the payoff. Let's look at a world where PHP is taught. Since PHP comes down from C, we have the same things other languages have.. logical statements and conditionals, loops, and OOP. We don't have support for short arrow syntax or generics yet but its coming. So we can start out with printing, looping, conditionals, and then move into something more robust. Out of the gate, you could layer the teaching with Slim PHP, a wonderful micro framework that is lightweight and mostly just a router. Couple that with a templating engine like Plates and you can build web pages. From there we can go into a bigger framework like Laravel. Love it or hate it, Laravel will get developers up and running fast. If the code schools worked in harmony with the PHP community, sending the students to user groups gets them involved quickly and you can find a mentor/mentee situation. If you get the community more involved, the businesses will follow as well. It was admitted to me that part of the reason my current company brought me on was for my community involvement. They wanted to be more involved with the community so having me around was a bridge to that. Think of how many other companies are waiting to be involved but don't have a person they can have on staff to help make that happen. 

The PHP Community needs to do a few things too. We need to revive PHP Mentoring and make it something we push hard. If you are a senior developer, a mid-level developer, or something more give an hour of your time. If you see someone on Twitter or elsewhere bashing PHP, just tell them times are a changing and it's getting better. A lot of these people had a bad experience and don't know PHP has gotten better. 

Boot camps and instructors: if you read this I would love to help. I know a lot of us would. Was I right in my assumptions? Am I missing something blatant you see that I don't? 

Companies: if you read this, where did I get it right and wrong? Is junior programmer burn out legit? Or are you doing what a lot of companies do.. piggybacking off OSS, not giving back and not helping us grow the language and community?

<3


Sources: 
* 1 - https://www.coursereport.com/blog/coding-bootcamp-cost-comparison-full-stack-immersives
* 2 - https://www.coursereport.com/coding-bootcamp-ultimate-guide
* 3 - https://www.codingdojo.com/blog/7-most-in-demand-programming-languages-of-2018/
