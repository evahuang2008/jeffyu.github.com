---
date: '2007-09-28 21:53:00'
layout: post
slug: implementing-a-jca-resource-adapter
status: publish
title: Implementing a JCA Resource Adapter.
wordpress_id: '155'
categories:
- Java
---

JCA(Java Connector Architecture) is a bridge that connect Exteranl System (i.e EIS) to App Server, so that they can communicate.  
We can split the connection into two categories.  
1. Outbound connection.  
This is App Server initialize the request to EIS. The flow is: App Server -> RA (resource Adapter) -> EIS.  
2. Inbound connection.  
This is EIS initialize the request to App Server. The flow is: EIS -> RA -> App Server.  
One thing needs to say, this is also called Message-Inflow support, (a.k.a MDB support), it is introduced in the JCA1.5. Here it considers the MDBean as an endpoint that accept the incoming Message which send from the EIS. The RA needs to establish a listener, whose responsibility is to accept Message from EIS, and then convert the Message to the MDBean acceptable Object if any, deliver the received Message to the MDBean.
