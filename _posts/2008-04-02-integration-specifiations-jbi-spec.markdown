---
date: '2008-04-02 18:41:00'
layout: post
slug: integration-specifiations-jbi-spec
status: publish
title: Integration Specifiations - JBI spec
wordpress_id: '193'
categories:
- Java
- SOA
---

As I said in the last entry, it has drawback in the JCA spec for Enterprise integration, besides, we can not put the JCA in the Message Oriented Middleware category, which JBI, JMS were in.  
  
Ok, today I am talking about the JBI spec, firstly it stands for Java Buisiness Integration, and it is a way to combine all the existing services. In the JBI Spec, we are talking about nothing but service, and the Message is the unit that we are exchanging.  
  
JBI as a container spec, its content can split into two category.  
1. Runtime  


  *   1) Normalized Message
  *   2) Normalized Message Router
  *   3) Component
  *       3.1 Binding Component -> which connects to the outside endpoint
  *       3.2 Service Engine  -> which locates in the ESB itself.
  *   4) DeliveryChannel
  *   5) Message Exchange Pattern
2. Management  


  * 1) Packaging
  * 2) Component installation
  * 3) Service deployment.
  * 4) Monitor
We can see that the management functionality is to help the runtime. The primary function of runtime is to route message from one component to another. Messages are delivered in a Normalized Message, which was described in WSDL2.0, and the Normalized Message Router are in charge of routing, you also can use servicemix-eip component or [Apache Camel](http://activemq.apache.org/camel) to help you build more complicated routing.  
  
JBI environment is consist of components, it makes no sense if there are no components. component can divide into two category in terms of logical functionality. One is Binding Component, which we can see as a bridge to connect the outside service. The other is the Service Enginee that located in its inner ESB.  
  
Once we have the Router, Component. we also introduce a channel, which called Delivery Channel in the JBI spec for communicating between Normalized Message Router and Components.  
  
At last, seems there are many kinds of message exchange categories, such as One-Way, Request-Response etc, we introduced a Message Exchange Pattern concept to represent this.  
  
Well, for the JBI 1.0, I think pros in it is: Normalized Message, Normalized Message Router. And things not good are: Component specific API, not easy to write a SU, SA..  
  
PS: Freeman and I wrote a presentation about Apache ServiceMix, which is JBI 1.0 compliant. you can download from [here](http://jeff.yuchang.googlepages.com/servicemix.pdf).
