---
date: '2007-11-22 20:36:00'
layout: post
slug: jms-introduction-part-2
status: publish
title: JMS introduction - part 2.
wordpress_id: '177'
categories:
- Java
tags:
- JMS
---

From the [first part of JMS introduction](http://jeffyuchang.blogspot.com/2007/11/jms-introduction.html), we have a basic idea of how to operate the message to broker. In this entry, I am going to talk about some advanced feature for JMS.
They are:



	
  * 1. Transactional operations

	
  * 2. Security

	
  * 3. Reliability

	
  * 4. Distributed Message.

	
  * 5. Message Selector


Some JMS term exploring:

1. Persistent & MessageDelivery

By default, we can consider "broker" as a message repository, but sometimes, we want to make sure our message is delivered ONLY_ONCE, and we want our messages still available even our broker crashed. For activeMQ case, there is a "persistent" property in the broker.

There is also a term called "MessageDelivery", it means whether this message need to be persistent or not. The main difference is that if you are using persistent delivery, messages are persisted to disk/database so that they will survive a broker restart. When using non-persistent delivery, if you kill a broker then you will lose all in-transit messages. [R1]

2. Acknowledge. (Recovery & Redelivery)
• AUTO_ACKNOWLEDGE or DUPS_OK_ACKNOWLEDGE - the message will be immediately redelivered. The number of times a JMS provider will redeliver the same message before giving up is provider-dependent. The JMSRedelivered message header field will be set for a message redelivered under these circumstances.
• CLIENT_ACKNOWLEDGE - the next message for the listener is delivered. If a client wishes to have the previous unacknowledged message redelivered, it must manually recover the session.
• Transacted Session - the next message for the listener is delivered. The client can either commit or roll back the session (in other words, a RuntimeException does not automatically rollback the session).

3. Durable & non-durable subscriber.
Queues retain all messages sent to them until the messages are consumed or until the messages  expire. while in Topic, There is a timing dependency between publishers and non-durable subscribers, because a client that subscribes to a topic can consume only messages published after the client has created a subscription, and the subscriber must continue to be active in order for it to consume messages.
A durablesubscriber registers a durable subscription with a unique identity that is retained by JMS. Subsequent subscriber objects with the same identity resume the subscription in the state it was left in by the prior subscriber. If there is no active subscriber for a durable subscription, JMS retains the subscription’s messages until they are received by the subscription or until they expire.

4.Transaction

There are two kind of transactions here: client -> broker & client -> broker -> client. In the JMS API, it just defines the former one. the latter one should be a two-phase commit transaction. Transaction was controlled by Session Object, it is very like Database's Connection, by using commit or rollback at last.

5. Message Selector
As we talked before, the broker holds the queue or topic, which holds the messages, so many messages, we need to define a criteria to select some appropriate messages that we are interested, here comes the MessageSelector, it uses SQL-92 compliant syntax, one thing to note is that it just selector the MessageHeader & Message Properties, not include the MessageBody.

Reference:
1. [ActiveMQ's message delivery](http://activemq.apache.org/what-is-the-difference-between-persistent-and-non-persistent-delivery.html)
2. JMS_1.1_specification
