---
date: '2007-11-17 03:56:00'
layout: post
slug: is-it-a-bad-idea-to-reply-on-spring-too-much
status: publish
title: Is it a bad idea to reply on Spring too much?
wordpress_id: '172'
categories:
- Thoughts
tags:
- Spring
---

Since spring is more and more powerful & popular, to some extent, it becomes the de facto JEE application's infrastructure, so a lot of projects in the open source area(Apache CXF, Apache Servicemix ...) use spring as its basic configuration & bean management... some of my colleagues said it was a bad idea that we rely on spring too much. I don't so, reasons are:



	
  1. Spring is open source, we can see how it gets the job done, we know how it works, we can modify it as what we want.

	
  2. Take Apache CXF for example, since now a lot of people are using spring, it is not a good idea to create another XSD or DTD to ask people to learn for configuration, always remember people are lazy, we need to reduce the learning curve. Since spring did a good job, at least, if you want to write a new one, you need to specify where the spring configuration can't meet your requirement..

	
  3. Some people think relying on spring too much, maybe one day, we will lose our place, since interface21 people (which create and provide support for spring) will take over our product... I don't agree with it, spring is good at one place, but it doesn't mean that they are good at everything, or they do not have time to take everything... look how eclipse and those eclipse plug-ins work together..


All in all, I don't think rely on spring too much is a bad thing, instead, I think we need to adopt those good libraries, not to write a new one simply because we are afraid that we might lose our place.. remember, open source software means you can see how codes work, you can change them.. Successful people always stand on a giant...
