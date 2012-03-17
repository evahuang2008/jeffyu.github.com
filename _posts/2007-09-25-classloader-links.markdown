---
date: '2007-09-25 03:25:00'
layout: post
slug: classloader-links
status: publish
title: ClassLoader Links
wordpress_id: '153'
categories:
- Java
---

Recently, I am working on implementing the JCA stuff, one thing is very important for me is about the ClassLoader. ClassLoader becomes more and more important as now we got a lot of middle-ware stuff. You know, software has the version, a specific software can have multiple version as time goes by, so different middle-ware software might use different jar version, it may caused something incompatible due to different version.(such as API changes etc).  
  
1. [Tomcat ClassLoader explained.](http://tomcat.apache.org/tomcat-5.5-doc/class-loader-howto.html)  
2. [JDK endorsed standards override mechanism.](http://java.sun.com/j2se/1.4.2/docs/guide/standards/index.html)  
3. [Extension Mechanism Architecuture](http://java.sun.com/j2se/1.4.2/docs/guide/extensions/spec.html)  
4. [Understanding J2EE Application Server Class Loading Architectures](http://www.theserverside.com/tt/articles/article.tss?l=ClassLoading)  
5. [EJB 2 and J2EE Packaging](http://www.onjava.com/lpt/a/onjava/2001/06/26/ejb.html)
