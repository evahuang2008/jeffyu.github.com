---
date: '2008-09-26 17:22:00'
layout: post
slug: using-jdocbook-to-write-documentation
status: publish
title: Using jdocbook to write documentation
wordpress_id: '217'
categories:
- Java
- JBoss
---

If you are trying to find a tool to write your project documentation, and you don't like to use word processor to write your articles, you know, it is web era, sometimes you won't just to have one output, and you don't want to stick to one particular format either. then the [JBoss Docbook](http://www.jboss.org/maven-jdocbook-plugin/) might be of your interest.

I used to use MS word to write articles, with a set of pre defined formats, such as Heading and so on, so that can produce a TOC (table of content). well, I still don't like to use Word to write articles. And then I find the [JBoss Docbook](http://www.jboss.org/maven-jdocbook-plugin/) is very good and easy to use.

Use the JBoss Docbook is quite easy, now it is mavenized. you just simply define dependency and then add the task in the build process, that's all. BTW, if you are using Linux box, you can open the doc by "Open with Help" without running mvn install to build it.

So personally, I use Eclipse, with Xmlbuddy plugin to write the document, and it works quite well.
