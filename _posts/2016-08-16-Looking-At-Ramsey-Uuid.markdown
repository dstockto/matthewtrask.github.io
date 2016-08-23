---
layout: post
title:  "Looking at Ramsey UUID"
date:   2016-08-16
comments: yes
description: My first post in a series with a look at a sweet Uuid library
tags: Php, Uuid, Open Source, Libraries, Programming
---

## Its all about that Uuid

Welcome to the first installment in my 2113918230981 part series, "Better know a Package!". Tonight's package: the famous/infamous Uuid package that that taught us all what Ramsey is in Scottish, Rhumsaa. Created to give PHP a libray to generate Universal Unique Identifiers, this library has been a stallwort in the community. Ben Ramsey created it first under the Rhumsaa namesapce before moving it to the Ramsey namespace, saving us all from learning more Scottish then we needed to ever learn. 

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
 


