---
date: '2010-01-22 19:39:00'
layout: post
slug: maven-global-excludes-tip
status: publish
title: Maven Global Excludes tip.
wordpress_id: '268'
categories:
- Maven
---

If you work on a project that has ton of jar dependencies, and you want to exclude the 'xerces' (for example), you might end up using the exclusion multiple times, as a lot of jars are depending on the 'xerces'. In this case, you can use [following way to achieve the 'global exclude' ](http://jlorenzen.blogspot.com/2009/06/maven-global-excludes.html)in maven.
