---
layout: post
title:  "Looking at Ramsey UUID"
date:   2016-08-22
comments: yes
description: My first post in a series with a look at a sweet Uuid library
tags: Php, Uuid, Open Source, Libraries, Programming
---

## Its all about that Uuid

Welcome to the first installment in my 2113918230981 part series, "Better know a Package!". Tonight's package: the famous/infamous [Ramsey\Uuid](https://github.com/ramsey/uuid) package that that taught us all what Ramsey is in Scottish, Rhumsaa. Created to give PHP a library to generate Universal Unique Identifiers, this library has been a stallwort in the community. Ben Ramsey created it first under the Rhumsaa namesapce before moving it to the Ramsey namespace, saving us all from learning more Scottish then we needed to ever learn. 

## What is an UUID?

A UUID, or Universally Unique Identifier, will generate a 128 bite unique key in different series based on the version you asked for. [RFC-4122](https://tools.ietf.org/html/rfc4122) dictates how Uuids should be generated, and recommends 4 types: a time and MAC address based uuid, a name based uuid with md5 hash, a random uuid and a name based uuid with sha1 hash. Each can be used however you want. So lets look as use cases and how we can utilize Ramsey\Uuid to build better software. 

## Uuid version 1 - As Time goes by

Uuid 1 is the time and MAC addressed based Uuid provided by Ramsey\Uuid. What this means is that if you run 

```
<?php

require __DIR__ . "/../vendor/autoload.php";

use Blog\Uuid\VersionOne;

$uuid1 = new VersionOne();

for($i = 1; $i <= 5; $i++){
    $uuid = $uuid1->uuid();
    echo $uuid . "\n";
}
```

and defined here:

```
<?php

namespace Blog\Uuid;

use Ramsey\Uuid\Uuid;

class VersionOne
{
    public function uuid()
    {
        $uuid = Uuid::uuid1();

        return $uuid->toString();
    }
}
```

it will return 5 uuids, as seen here:

```

/**
 * Uuid1
 * e110806e-68d3-11e6-98c2-f45c89b67421
 * e1108ac8-68d3-11e6-9525-f45c89b67421
 * e1108d02-68d3-11e6-b0ca-f45c89b67421
 * e1108f14-68d3-11e6-98b1-f45c89b67421
 * e1109112-68d3-11e6-b0ae-f45c89b67421
 */
 ```
 
 You can see both differences and similarities with the 5 uuids returned. This type of uuid creates a Uuid based on a single point of time on one computer. The plus is that since time never goes backwards, you wont get a collision of uuids. One thing to take into mind is that while computer do not share a MAC Address, they can be spoofed, thus potentially causing a collision of uuids. While this is very rare, it is a possibility in terms of security. 
 
## Version 2
 
There is a verion 2? Of course! Its set for DCE, but not an implementation of RFC 4122, so we wont worry about it. But if you want to learn something more, check it out!

## Version 3

With version 3, we create uuids based on a namespace and then it is md5 hashed. For this example I ran my blog, ```http://matthewtrask.net``` as the namespace to uuid.

```
<?php

namespace Blog\Uuid;

use Ramsey\Uuid\Uuid;

class VersionThree
{
    public function uuid()
    {
        $uuidV3 = Uuid::uuid3(Uuid::NAMESPACE_DNS, 'http://matthewtrask.net');

        return $uuidV3->toString();
    }
}
```

and the bootstrap is:

```
<?php

require __DIR__ . "/../vendor/autoload.php";

use Blog\Uuid\VersionThree;

$uuid3 = new VersionThree();

for($i = 1; $i <= 5; $i++){
    $uuid = $uuid3->uuid();
    echo $uuid . "\n";
}
```

which will return 

```
/**
 * Uuid3
 * 51e103b4-5333-388c-b72f-c362929a2b1f
 * 51e103b4-5333-388c-b72f-c362929a2b1f
 * 51e103b4-5333-388c-b72f-c362929a2b1f
 * 51e103b4-5333-388c-b72f-c362929a2b1f
 * 51e103b4-5333-388c-b72f-c362929a2b1f
 */
 ```
 
 So what do we learn here? Well, Uuid::uuid3() is not random. It is generated based on what is inputted. So should we change the namespace to lets say: ```https://waltdisneyworld.com``` we get the following:
 
 ```
 /**
 * WDW Uuid 3
 * f815042b-3562-3d0d-8aea-e2ebf858725d
 * f815042b-3562-3d0d-8aea-e2ebf858725d
 * f815042b-3562-3d0d-8aea-e2ebf858725d
 * f815042b-3562-3d0d-8aea-e2ebf858725d
 * f815042b-3562-3d0d-8aea-e2ebf858725d
 */
 ```
 
 Notice how all values change based on input, but they repeat for the inputed value. 
 
## Version 4 - Super Duper So Rad Random
 
 Uuid version 4 is currently the one my company uses to identify all the things. Its great because its random. Its the perfect id mechanism. Even better, its great for exposing things to the world without others being able to run a script against our APi and get a general idea of the size of our DB. [Phil Sturgeon](https://twitter.com/philsturgeon) writes about why we should expose uuids over ids in [this article he wrote](https://philsturgeon.uk/http/2015/09/03/auto-incrementing-to-destruction/). So lets see what we get returned to us when we run this script. 
 
 ```
 <?php

namespace Blog\Uuid;

use Ramsey\Uuid\Uuid;

class VersionFour
{
    public function uuid()
    {
        $uuid = Uuid::uuid4();

        return $uuid->toString();
    }
}
```

with the bootstrap:

```
<?php

require __DIR__ . "/../vendor/autoload.php";

use Blog\Uuid\VersionFour;

$uuid4 = new VersionFour();

for($i = 1; $i <= 5; $i++){
    $uuid = $uuid4->uuid();
    echo $uuid . "\n";
}
```

returns to us:

```
/**
 * Uuid v4
 * 151f8d47-99c3-43c9-8993-e0ffb3a7704d
 * a45c23a6-ad73-4417-aff9-604c4c195580
 * f0668777-0ea5-4503-8ffe-abc3e740f553
 * 64067149-1804-4f71-b754-38765add464b
 * f4c5e9e0-d1a6-4cf1-b69b-4815439f4091
 */
 ```
 
 As you can see there thery are random, with from what I can see, only spot in the uuid sharing the same number across all 5 generated uuid's. We will talk about use cases in a bit, but I wanted you to notice that this has so much potential for many different use cases in your application. 
 
## Version 5

Version 5 of the Uuid spec is extremely similiar to Version 3 in that it is namespace based but instead of using md5 it utilizies the sha1 hash. Lets take a look:

```
<?php

namespace Blog\Uuid;

use Ramsey\Uuid\Uuid;

class VersionFive
{
    public function uuid()
    {
        $uuid = Uuid::uuid5(Uuid::NAMESPACE_DNS, 'http://matthewtrask.net');

        return $uuid->toString();
    }
}
```

with the bootstrap:

```
<?php

require __DIR__ . "/../vendor/autoload.php";

use Blog\Uuid\VersionFive;

$uuid5 = new VersionFive();

for($i = 1; $i <= 5; $i++){
    $uuid = $uuid5->uuid();
    echo $uuid . "\n";
}
```

which returns to us:

```
/**
 * Uuid5
 * 0fcbe08b-1a1b-552a-8406-9c68e20106f6
 * 0fcbe08b-1a1b-552a-8406-9c68e20106f6
 * 0fcbe08b-1a1b-552a-8406-9c68e20106f6
 * 0fcbe08b-1a1b-552a-8406-9c68e20106f6
 * 0fcbe08b-1a1b-552a-8406-9c68e20106f6
 */
 ```
 
 Again, all 5 are the same, cause its based on the input. I passed ```http://matthewtrask.net``` and get the uuid backed based on that namespace. 
 
## Use Cases for Uuids

After looking at the 4 types of Uuid's the Ramsey\Uuid library provides, its time to look at how you want to use these. Its simple to look at version one and say that you can use that to identify work stations in a data center or enterprise level business with hundreds of work stations. But you should take note, that this isnt a Uuid you should use for security, its guessable through MAC Address sppofing. 

For version's 3 and 5, the fun thing is that they are completely reproducable with the same algorithm. So if you lose the Uuid, you can re-generate it with the same code provided you still have the code laying around. Now why would you use this? Thats one thing Im looking at. I guess you could use it to securely pass around website ideas on the open web, but unless you are trying to hide the website from public view then you shouldnt have it on the open web. If you have a list of websites from where people are coming from, you can run a check against uuid's in that sense, but I dont think that creates a good use case. 

Version 4 is the one most people use and its easy to see the use case here. As the Phil Sturgeon article points out, using and exposing an auto-incrementing id through an API is a fast way to let the competition run a script against the endpoint and get a rough esitmate of your database. So this works in protecting your database and user base from competition trying to size you up. Also, using an Uuid v4 allows for greater uniqueness. Rather then come up with a complex id system to track the various id's floating in your system (user_id/job_id/transaction_id), you can create a ```Uuid::uuid4()``` for each one and never have to work on concurrent id's across a system. 

## Thoughts

As I finish up the first installment of my 1231923808 series of "Better Know a Library!", it was a lot of fun to look deeper in to Uuids. Ive seen Ben give a talk about Uuid's, but running scripts to see them for myself greatly helped me understand them better. 

Until next time, have fun uuid-ing everything in your system!


