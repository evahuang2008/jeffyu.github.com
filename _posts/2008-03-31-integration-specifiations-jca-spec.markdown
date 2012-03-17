---
date: '2008-03-31 17:27:00'
layout: post
slug: integration-specifiations-jca-spec
status: publish
title: Integration Specifiations - JCA spec
wordpress_id: '192'
categories:
- Java
- SOA
---

In this series, I am going to talk about three Java Specifications, they are JCA, JBI, JMS spec. I would say these three specs are all for integrating with exsiting legacy system, such as Enterprise Information System(EIS).  
  
Firstly, lets see what JCA spec is about. Before the JCA spec was introduced, the vendors were using their own proprietary API to do the integration, and it was non-portable, I mean, switch from different Application Servers.  
  
So here comes the specification that tries to build a standard API to solve the portable problem as JavaEE did. The JCA spec is consist of two participants. one is Application Server Vendor, the other is Resource Adapter provider.  
  
For the application server vendor, most part of job is to support the resource adapter deployment. so I will examine the spec from resource adapter provider's perspective.  
  
Here is the list that resource adapter needs to accomplish, it falls two main buckets:  
  
1. Outbound Connection. (outside systems initiate data request to your system).  


  *   1). Connection Management Contract
  *   2). Transaction Management Contract
  *   3). Security Management Contract
2. Inbound Connection. (your system initiates data request to other systems)  


  *   1). Lifecycle Management Contract.
  *   2). Message Inflow Contract.
It seems that JCA spec would solve the integration against legacy systems, the truth is that the JCA spec is  designed to support the traditional request-response model, but fails to support complex long running transactions and integrations scenarios, because most of integration scenarios like to support it in asynchronous way.  
  
So here comes to JBI spec that tries to rescue, which I am going to describe in next entry....  
  
References  
[1] [connect the enterprise with JCA.](http://www.javaworld.com/javaworld/jw-11-2001/jw-1121-jca.html?page=1)
