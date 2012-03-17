---
date: '2007-09-28 15:12:00'
layout: post
slug: write-your-own-classloader
status: publish
title: Write your own ClassLoader
wordpress_id: '154'
categories:
- Java
- Thoughts
---

In general, classLoader is using the parent-first algorithm, which means if you want to load a Class, it will find the parent ClassLoader (it doesn't mean it is parent-class), if the parent ClassLoader doesn't find the specified Class, and then it tries to load class in the child classLoader.  
So when you need to write your own ClassLoader? if you want to implement child-first classloader algorithm, then you need to write. A typical scenario is the Application Server that you are using is using older third party jar than you need for your APP.  
  
Two links about custom classloader:  
1. [Find a way out of the ClassLoader maze](http://www.javaworld.com/javaworld/javaqa/2003-06/01-qa-0606-load.html)  
  
2. [Get a load of that name](http://www.javaworld.com/javaworld/javaqa/2003-03/01-qa-0314-forname.html)!
