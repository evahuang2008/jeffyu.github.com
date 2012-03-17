---
date: '2007-11-18 22:22:00'
layout: post
slug: guice-simplicity-impressed-me
status: publish
title: Guice simplicity impressed me.
wordpress_id: '175'
categories:
- Java
tags:
- Guice
- IOC
---

Today, I've tried a simple sample with [Guice](http://code.google.com/p/google-guice/), it reduces a lot configuration compares to spring's xml config. Firstly, I am a bit of worrying using annotation too much would make code a bit messy, it would be a bit hard to read with a lot of annotation, that fact is that with Guice, it is not too much annotation, we can consider it is sort of javadoc, and just for the resource that you need to inject.

Compared to spring's xml configuration, it has below advantages (IMHO) :
1. Use the @Inject annotation to define the injections, instead of using xml, for xml configuration, you need to write verbose xml to define the relationship.
2. The string in the xml file is more misspelling than using java code itself, since compiler would tell you that.
3. The most important one is it can make them consistent. It is easy for developers to refactor. Most IDE support that. I mean using java config instead of xml.. not the annotation.

There is a comprehensive comparison between Guice and Spring [here](http://code.google.com/p/google-guice/wiki/SpringComparison).

All in all, its simplicity impressed me, if you are looking for a lightweight DI container, you should check out Guice. It worths you a try.

PS: Spring also has the spring java config since 2.5 version, haven't got a chance to try it out yet.
