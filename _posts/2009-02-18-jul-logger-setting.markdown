---
date: '2009-02-18 04:13:00'
layout: post
slug: jul-logger-setting
status: publish
title: JUL Logger setting
wordpress_id: '225'
categories:
- Java
---

Well, first I have to say that the log in Java is kind of messy, why? we got too many choices. say log4j, jakarta common logging, slf etc. And as comes with the JDK 1.5, we have the java.util.logging along with this. Come on, it is just a simple log, what the hell do we need to have these many libraries.  
  
Anyway, avoid the jar conflictions, the simplest scenario would be to pick up the java.util.logging, as it has been shipped within JDK. If you are wondering where/how to update the logging.properties file, (like log4j.properties in log4j), then here we've got [a good article](http://www.ociweb.com/mark/programming/JavaLogging.html) [1] can help you.  
  
HTH.  
  
[1] In this article, for the 2nd method of updating logging.properties file, which should be located in the $JDK_HOME/jre/lib/logging.properties.
