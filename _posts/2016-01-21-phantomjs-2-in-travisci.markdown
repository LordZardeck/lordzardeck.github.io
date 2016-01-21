---
layout: post
title: "PhantomJS 2 in TravisCI"
modified:
categories: 
excerpt: PhantomJS 2 doesn't work out of the box with Travis, today I figured out how
tags: [travis ci, phantomjs, phantomjs2]
date: 2016-01-21T00:15:18-07:00
---

We recently added unit tests to our project, and ran them with Karma off of PhantomJS. After hours of frustration we discovered that the 1.x version of PhantomJS did not support some basic ES5 functionality, such as `Function.prototype.bind`. We also learned taht there was a 2.x unstable version of PhantomJS that did support this requirement, so we proceeded to update to `karma-phantomjs2-launcher`. This all worked fine on our local machines, and we went on our merry way, continuing to add tests.

Once we were finished, we pushed to GitHub our changes, and awaited Travis to show us that beautiful green build notification. Instead we got red. 

Unfortuanetly PhantomJS isn't supported out of the box on Travis. After scouring the dark corners of the web, we gave up trying to get PhantomJS 2 to run on Travis' containers and reverted back to their legacy system, installing shared library depencies and the like, and finally got our builds working. Although they took _forever_ to run.

## Light at the end of the tunnel

After being frustrated by the recent issues with Travis not building legacy builds, I took up arms again and fought to find a solution to running PhantomJS 2 on Travis containers. A Travis representitve offered a snippet of code to go our `.travis.yml` file, but no such luck. 

> Addition to .travis.yml file from Travis representitive:

{% highlight yaml %}
install:
  - mkdir travis-phantomjs
  - wget https://s3.amazonaws.com/travis-phantomjs/phantomjs-2.0.0-ubuntu-12.04.tar.bz2 -O $PWD/travis-phantomjs/phantomjs-2.0.0-ubuntu-12.04.tar.bz2
  - tar -xvf $PWD/travis-phantomjs/phantomjs-2.0.0-ubuntu-12.04.tar.bz2 -C $PWD/travis-phantomjs
  - export PATH=$PWD/travis-phantomjs:$PATH
{% endhighlight %}

After continuing the discussion, they pointed out the fact that one of our node modules was re-installing PhantomJS, back to an unsupported build. That's when things started rolling toward victory.

# The final solution

After exploring the packages installed by `karma-phantomjs2-launcher`, I came across the `phantomjs-ext` package and their npm page: https://www.npmjs.com/package/phantomjs2-ext. Reading through the docs, I noticed we could specify a custom version through an environment variable. Sure enough, specifying version `2.0.0` for `PHANTOMJS2_VERSION` in travis's environment variables unlocked the blazing speed of contianers. Our quest was over.

# TL;DR

So if you are looking to add PhantomJS 2 to your Travis builds, there are 2 things you need to do:

1. Install the supported build of PhantomJS 2 from travis's s3 bucket and add it to the path
1. Add an environment variable to Travis specifying the PhantomJS version you installed

## .travis.yml file
{% highlight yaml %}
install:
  - mkdir travis-phantomjs
  - wget https://s3.amazonaws.com/travis-phantomjs/phantomjs-2.0.0-ubuntu-12.04.tar.bz2 -O $PWD/travis-phantomjs/phantomjs-2.0.0-ubuntu-12.04.tar.bz2
  - tar -xvf $PWD/travis-phantomjs/phantomjs-2.0.0-ubuntu-12.04.tar.bz2 -C $PWD/travis-phantomjs
  - export PATH=$PWD/travis-phantomjs:$PATH
{% endhighlight %}

## Travis environment variable
{% highlight bash %}
PHANTOMJS2_VERSION="2.0.0"
{% endhighlight %}