---
title: What am I thinking about Heroku?
date: 2017-11-25
updated: 2018-03-24
layout: post
tags: Heroku
---

## Why programmer prefer PaaS/Heroku (Platform as a Service)?

### Simple answer

It is so simple to use. That's it.

__First of all__, this article is not writing for professional purpose, marketing, ad. This article is based __my own experience__ with Heroku PaaS.

## Long answer

They don't need to know about sysadmin stuffs. Like  network management, load balancing, virtualizations, Unix/Linux security...

They can just focus own apps, that's why they don't lose their times to build a server, system or what they build.

![PaaS vs Others](https://mycloudblog7.files.wordpress.com/2013/06/screen-shot-2015-06-09-at-2-13-05-pm1.png)

As you can see in the picture, you just manage an application. OK, this is not big deal for if somebody who does not know about SaaS/PaaS/IaaS ecosystem. But if you want to know "what's going on" in Heroku, I'll tell you.

## Heroic or Haiku?
The name is not matter but you curious about the name where came from, you can check this the [wikipedia.org](https://en.wikipedia.org/wiki/Heroku#Etymology) link.

## Heroku?
This is a PaaS provider for application which works with HTTP.I have used the service since 2015 for my basic web applications demos/test. And it is pretty good. I don't pay anything for this service. I just confirm my credit card, because they offered free time for free dyno if I confirm. Anyway Let's get in, next part is "what should I know?".

## What should I know - Should I be a programmer?
NOPE. But you have to have little bit terminal experience, because Heroku works (not only) with CLI. Also you can manage your application very limited. For example, you can scale your application but you can not push (aka. git terminology) it.

You can sign up and make a free demo blog site, free demo wiki site.

> "Hey Berkhan, why did you say "DEMO"?"

Because the service, free plan is not for (__in my opion__) production stage. The plan for demonstration, testing and other development stuffs. For example, you want to use Drupal. You have to buy, shared hosting, AWS or build your own local server. This are crazy, but if you know git (also see: [git](https://git-scm.com/)) you can build your own demo server in a minute.

OK, I know. AWS, Azure, Google Cloud or DigitalOcean offer in 1 minute a server deploying, but you are missing this point.

They are offering deploying __a server__. OK, (for example) Digital Ocean can build a WordPress, or Nginx server in 55 seconds but you will pay in a month $5 which is not bad. Right?

Anyway, I just want to say this

> If you buy cheaply, you pay dearly.

## Am I prefer Heroku?
YES,

Because (__in my opinion__), you can manage your application so easy, than others alternatives. You can add add-ons (element). Also you can make an add-ons.

In addition, free and hyobist dynos are really good if you want to start, but you don't have any idea about PaaS.

But!

If your application will grow day after day, you have really big problem.

Price.

It's very expensive if you will use professional dynos (per dyno $25-$500 month) than IaaS providers. But, I'll give you the solution. You can use open source PaaS solution (Google it).
