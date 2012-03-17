---
date: '2007-07-21 17:00:29'
layout: post
slug: java-util-concurrent%e5%8c%85
status: publish
title: java.util.concurrent包
wordpress_id: '15'
categories:
- Java
---

这几天,在看java.util.concurrent包,我以前一直以为说,JDK1.5中相比1.4来说,无非就增加两个:一个是Generic,一个是Annotation,但是,前段时间在看CXF的源代码的时候,需要研究到Executor,以及AtomicReference类等..才发现,在多线程方面,JDK1.5比JDK1.4进步了很多,巨多..其中那个包的代码大多来自Doug Lea的作品..也正是有了JDK1.5 concurrent包,Java就又有了一个叫non-blocking的概念.  
下面是我这段时间看的觉得不错的一些资源  
[<concurrency in JDK1.5> PDF](http://www.few.vu.nl/~tzolov/links/java1.5-concurrency-IBM-tutorial.pdf)  
还有一些来自Brian Goetz在IBM developerworks上写的文章:  


  1. [Introduction to nonblocking algorithms](http://www.ibm.com/developerworks/java/library/j-jtp04186/index.html?S_TACT=105AGX02&S_CMP=EDU)
  2. [More flexible, scalable locking in JDK 5.0](http://www.ibm.com/developerworks/java/library/j-jtp11234/)
  3. [Going atomic](http://www.ibm.com/developerworks/java/library/j-jtp11234/)
