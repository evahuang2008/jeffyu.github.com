---
date: '2007-11-22 19:03:00'
layout: post
slug: jms-introduction
status: publish
title: JMS introduction
wordpress_id: '176'
categories:
- Java
tags:
- JMS
---

JMS(Java Messaging System)

Firstly, we will split this into three categories:
1. JMS client.
2. JMS API.
3. JMS provider.

Franky, I am quite confused about this when I first get touched on this subject, but after I compared JMS to JDBC, then all things become more clear, and easy to understand. we can think JMS provider as the database vendor, such as Oracle, Mysql etc. the JMS API is similar to the JDBC API, which is used to define a uniform interface to operate Message. The invocation should be like:


> JMS client -> JMS API -> JMS Provider.


In this entry, I am going to focus on the JMS API, since that's the developer most care about. before doing that, I am going to say a few words on the JMS Provider.
1. In the JMS world, we call the "JMS provider" as "message broker".
2. Message broker can be started as a standalone, or could be embedded too.

OK, just like the database, after you installed the database, you need to create the database instance, and the connection configuration, so that client can access the database by using JDBC API. so does JMS. but in the JMS world, it is called administered object. they are:



	
  * ConnectionFactory - This is the object a client uses to create a connection with a provider.

	
  * Destination - This is the object a client uses to specify the destination of messages it is sending and the source of messages it receives.


One thing that is very different from database world, it is that in the Messaging world, they are two messaging style(Domain): they are PTP (point-to-point) and Pub/Sub(Publisher-subscriber). The difference between these two styles are: in PTP, one message just can be consumed by ONE consumer; while in the Pub/Sub, a message can be consumed by Multiple consumers.
So you would see two separate APIs for PTP and Pub/Sub respectively in the JMS API, I will use the common one in my next of this entry.

In the database world, we are operating data in database record as a basis, in the JMS, we are using a javax.jms.Message as a basis. Right now, it has 5 subclass of this class, which supports Text,Object,Stream,Map,Byte as transmit unit. In this Message model, it is consist of Message Header, Message Properties, Message body.

Developers can retrieve/update data from JDBC API, so does JMS API, developers can produce(publish)/consume(subscribe) data, which is Message, from JMS API.  In order to be a producer or consumer, you need to obtain below two objects.

	
  * Connection: A JMS Connection is a client’s active connection to its JMS provider. It will typically allocate provider resources outside the Java virtual machine. A Connection is a factory for Sessions that use its underlying connection to a JMS provider for producing and consuming messages.

	
  * Session: A JMS Session is a single-threaded context* for producing and consuming messages. Although it may allocate provider resources outside the Java virtual machine, it is considered a lightweight JMS object.


and then you can create producer or consumer from Session & Destination Objects. For the consumer, it has two consuming style: Synchronous & Asynchronous.

A simple example for producing a message using ActiveMQ.(A JMS provider):


> // Create the connection.
ActiveMQConnectionFactory connectionFactory = new ActiveMQConnectionFactory(user, password, url);
connection = connectionFactory.createConnection();
connection.start();

// Create the session
Session session = connection.createSession(transacted, Session.AUTO_ACKNOWLEDGE);
destination = session.createQueue(subject);

// Create the producer.
MessageProducer producer = session.createProducer(destination);
producer.setDeliveryMode(DeliveryMode.NON_PERSISTENT);

// Start sending messages
TextMessage message = session .createTextMessage();
message.setText("producing message");
producer.send(message);

//Closing resources, it is better put this in finally block.
session.close();
connection.close();


Reference
1. [JMS slides from javapassion.com](http://www.javapassion.com/j2ee/JMS_speakernoted.pdf) (Highly recommend).
2. [Java messaging service API from JavaEE 5 tutorial](http://java.sun.com/javaee/5/docs/tutorial/doc/bncdq.html)
