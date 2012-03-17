---
date: '2007-11-07 02:46:00'
layout: post
slug: osgi-doesnt-look-up-class-in-its-own-package
status: publish
title: OSGI doesn't look up class in its own package.
wordpress_id: '163'
categories:
- Java
- OSGi
---

Today I am trying the sample code from [this article.](http://www.eclipsezone.com/eclipse/forums/t90796.html).  
  
Say, I am exporting one package as: com.example.movies. Then I write another bundle called FlatMovies.jar that contains a class inside com.example.movies(say package as the exported one).  
  
In this situation, I would get a ClassNotFoundException when I try to start the FlatMovies bundle..  
  
Not sure why, here make it a note.
