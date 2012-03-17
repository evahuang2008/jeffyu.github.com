---
date: '2007-11-17 02:15:00'
layout: post
slug: spring-1-2-x-ioc-exploring
status: publish
title: Spring 1.2.x IOC exploring
wordpress_id: '171'
categories:
- Java
tags:
- IOC
- Spring
---

Spring uses bean factory to manage the application beans.  what we most uses is using the xml config file to define the beans dependency and initializations..

Here I do not want to elaborate the whole config thing, there are a lot of material in the Internet and Reference, which did a better job than me, I just want to list some features that you might not use that often, and might don't know it yet.



	
  1. Bean's auto-wiring. (By Name, By Type, Construcotor, auto-detect).. but here I think it is better for us to wire beans explicitly. But if you are a COC fan, then you might be like this functionality.

	
  2. Bean creation by static factory method or by instance factory method. In most of cases, we are using bean creation by constructor, but for legacy codes integration, we might need the other two options.

	
  3. Method Injection, by using look-up method Injection & arbitrary method replacement.

	
  4. "depends-on" attribute, in case there is a bean rely on other bean's initialization.

	
  5. Lifecycle interfaces. (InitializatingBean, DisposableBean) or using init-method, destory-method in config file.

	
  6. Aware-suffix interface, such as BeanFactoryAware, ApplicationContextAware... if you want to get the BeanFactory or ApplicationContext object in your bean, such as publish events in the applicationContext, you can implement *Aware interface to get it. Spring will populate the context to your bean.

	
  7. FactoryBean. This one is quite easy to get confused by the BeanFactory at first glance. They are totally different.. BeanFactory is managing beans.. FactoryBean just take charges of creating a bean. Remember in most cases, we are creating a bean via constructor..what if we want to create a proxy class, which target is the bean's instance.. Then implements the FactoryBean's interface to do that. (commonly, it is used in the spring's library itself, such as AOP proxy class, JndiObjectFactoryBean and so on.


Reference:
1. [Spring 1.2.x Reference](http://static.springframework.org/spring/docs/1.2.x/reference/beans.html)
2. <<Expert one-on-one Design and Development>> chapter 11.
3. [Java Passion Free course](http://www.javapassion.com/j2ee/#Spring_Framework_Dependency_Injection)
