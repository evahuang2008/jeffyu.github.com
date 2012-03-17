---
date: '2007-11-18 04:02:00'
layout: post
slug: spring-2-x-ioc-exploring
status: publish
title: Spring 2.x IOC exploring
wordpress_id: '173'
categories:
- Java
tags:
- IOC
- Spring
---

OK, Lets see how the IOC (DI) module move forward in the spring 2.x version.



	
  1. XML configuration extensions. 

I would say this enhancement make the third-party library, which build on spring's IOC container, a lot of easier for the configuration. Such as Apache CXF, Apache Activemq and so on. Personally, I would consider this is a big improvement for the configuration, and integration with other libraries.
Adding a custom xml configuration typically has below four steps:

	
    * Authoring an xml schema to describe your custom element(s).

	
    * Coding a custom NameSpaceHandler implementation.

	
    * Coding one or more BeanDefinitionParser implementation. (This is the real job that need to be done. populate the data from xml file).

	
    * Registering the above artifact with spring.


The most real job is parsing the xml in the BeanDefinitionParser class, and get the data from xml to bean.

The spring's registering way is an inspiration of how we can register the stuff modularly, instead of putting all of configuration file in one center place, we can split them in its own module, but with the same relative path, such as /META-INF/spring/spring.handlers for spring's example.

	
  2. New Bean scopes.
In the Spring1.x IOC module, it just has two scope:the singleton and non-singleton, it is way too coarse-grain. In the 2.x version, it adds more scopes, like Session scope, Request scope etc..it also has custom scope.

	
  3. Spring Java config.
To be specific, this is introduced by the spring2.5.. I am gonna try this later and give it a comparison with [Guice](http://code.google.com/p/google-guice/) in next couple entries..


Reference
1. [Spring 2.x extensible xml explanation](http://static.springframework.org/spring/docs/2.0.x/reference/extensible-xml.html)
2. [spring-components-xml-configuration-on-steroids (example)](http://www.memestorm.com/blog/spring-components-xml-configuration-on-steroids/)
3. [Spring2.o Intro](http://www.infoq.com/articles/spring-2-intro) (Posted at InfoQ)
4. [How CXF configuration works](http://cwiki.apache.org/CXF20DOC/configuration-for-developers.html)
5. [Spring Java config reference](http://static.springframework.org/spring-javaconfig/docs/1.0-m2a/reference/html/)
