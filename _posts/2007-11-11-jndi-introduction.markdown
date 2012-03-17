---
date: '2007-11-11 06:21:00'
layout: post
slug: jndi-introduction
status: publish
title: JNDI introduction
wordpress_id: '166'
categories:
- Java
---

If you are using EJB, you must be familiar with JNDI concept, since if you want to find a EJB Remote Object, you need to obtain the object through JNDI..
Yes, I know JNDI, it is a naming service and directory service for EJB, that was my original thought and understanding on JNDI. JNDI is so simple that I could imagine that and I don't even need to take a look at some related materials on it, we can get its meaning from the name itself. So it gives me an impression that the JNDI is belonged to the EJB, if you want to use JNDI, you need to start the EJB container, which I really don't like to do that today. (I'm a POJO fans, the deploy-redeploy cycle test is really a time-consuming, low productivity stuff).

Today, I am looking on the JMS stuff, which I need to talk with JNDI again, from my original understanding, I need to start the EJB container to use JNDI, then I found the tutorial[1] from SUN, and then I found my original understanding was wrong, JNDI is not belonged to EJB, we just can say EJB uses JNDI by providing RMI JNDI spi.

The JNDI offer two functionalities:
1. Name & Naming service.
2. Directory & Directory Service.

It is also involved with two Interfaces:
1. API. Application Programming Interface.
2. SPI: Service Providing Interface.

So, for the EJB case, it provides the RMI as SPI implementation; for the JMS case, its implementation, such as ActiveMQ, will provide the JNDI SPI implementation.

Lets see how we get a Object from JNDI typically:
[java]
Hashtable env = new Hashtable();
env.put(Context.INITIAL_CONTEXT_FACTORY,"com.sun.jndi.fscontext.RefFSContextFactory");
Context ctx = new InitialContext(env);
Object obj = ctx.lookup(name);
System.out.println(name + " is bound to: " + obj);
ctx.close();
[/java]
We set the "INITIAL_CONTEXT_FACTORY" in the environment, which is the SPI's implementation's class. we might need to set other properties that the SPI's implementation need through the "key-value" in the environment, such as provider url, username, password etc.

Reference
1: [Sun's JNDI tutorial](http://java.sun.com/products/jndi/tutorial/trailmap.html)
