---
layout: post
title:  "PHPUnit - The German Way to Clean Code"
date:   2016-08-27
comments: yes
description: Hi, Im Matt and I like testing code
tags: Php, PHPUnit, Open Source, Libraries, Programming
---

## $this->assertTrue('I always test');

Welcome back folks! Now, when I started this, I figured I would start with some cool libraries on the smaller side. Libraries that compliment Application Development but aren't needed 100% of time. But after this delicious cup of coffee I decided to do it. So tonight, in the second part of my 239082304982 part series "Better know a Package" we look at [PHPUnit](https://phpunit.de)

Started back on a dare from his comp sci professor, the soft spoken [Sebastian Bergmann](https://twitter.com/s_bergmann) set out to write an xUnit style test suite for his beloved PHP. With the birth of PHPUnit, PHP was pushed forward into a new era, with tests complimenting the code and making it so that we didnt always have to refresh the browser or network tab to see if our output was correct. Lets take a deeper look at this library and see what we can do, and how we can use it to frustrate our bosses when we say "it needs more tests".

## PHPUnit and PHPUnit.xml

As of now, we are on version 5.5.x of PHPUnit. Sebastian has set himself a timeline of a major version release each year. With 4.8 in Long Term Support and Sebastian being a stickler for SemVer, you really dont have much of a reason to at least be on 4.8. Setting up PHPUnit is straight forward. It takes the following:
```
composer require-dev phpunit/phpunit
```

and it is now in the dev section of your composer.json file. Next, you should set your autoload-dev to where you want your tests to live, like so:

```
"autoload-dev": {
    "psr-4": {
        "App\\Test\\": "tests/"
    }
}
```
and you are good to go on the installation!

Now, I will say that if you do not use composer (why the hell not?) or want to bring in the whole .phar file, there is instructions on the phpunit.de site that instruct you on how to do that.

To run PHPUnit, it takes a simple config file using XML. Ah yea, XML, that old format that new age developers hate, and older developers just say "meh". A sample XML config will look like this:

```
<?xml version="1.0" encoding="UTF-8"?>
<phpunit colors="true" bootstrap="vendor/autoload.php">
    <testsuites>
        <testsuite name="all">
            <directory suffix=".php">tests/</directory>
        </testsuite>
    </testsuites>
    <filter>
        <whitelist>
            <directory suffix=".php">src/</directory>
        </whitelist>
    </filter>
    <logging>
        <log type="tap" target="build/report.tap"/>
        <log type="junit" target="build/report.junit.xml"/>
        <log type="coverage-html" target="build/coverage" charset="UTF-8" yui="true" highlight="true"/>
        <log type="coverage-text" target="build/coverage.txt"/>
        <log type="coverage-clover" target="build/logs/clover.xml"/>
    </logging>
</phpunit>
```

The first thing to note is our bootstrap. We are telling PHPUnit that it should use the Composer autoload.php found in ```vendor/```. The test suite and filter sections should be self-explainatory but we are telling it the tests live in ```tests/``` and the code we are testing on is in ```src/```. Dont worry, PHPUnit is strict, like German strict. So if you get it wrong, it'll complain and tell you what you did wrong. 

The next part is the logging. This is an optional set of flags you can set if you want the HTML/Clover code coverage. And we will talk about that more in depth. But it has colors, which is highly appealing to people who aren't developers.
