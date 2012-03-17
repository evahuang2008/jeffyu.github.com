---
date: '2005-05-19 10:28:10'
layout: post
slug: web-application
status: publish
title: Web Application
wordpress_id: '136'
categories:
- Java
---

Web Application 这里指的是有Java环境的Container ,小型的如Tomcat ,Jetty ，大的比如Weblogic,JBoss,Websphere等.这边要关注的是WEB-INF/这个文件夹,我们用普通的url方式是访问不到里面的文件,但可以通过container来访问,所以里面可以放配置文件和我们要用到的类.那么container的装载顺序是先装载WEB-INF/classes/的目录，而后在装载WEB-INF/lib/.

A web application is a collection of servlets, html pages, classes, and other  
resources that make up a complete application on a web server. The web application  
can be bundled and run on multiple containers from multiple vendors.  
.................  
  
具体请参考Servlet_2.3_specification第9章 Web Application Chapter
