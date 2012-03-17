---
date: '2008-04-14 18:14:00'
layout: post
slug: brief-introduction-on-the-ws-cdl
status: publish
title: Brief Introduction on the WS-CDL
wordpress_id: '197'
categories:
- SOA
tags:
- WS-CDL
---

Because of the work's need, I need to work on the integration between the [WS-CDL Tool](http://pi4soa.wiki.sourceforge.net/) and [JBoss ESB](http://www.jboss.org/jbossesb), and here comes the chance that need to take a look at the WS-CDL specification.

Why the WS-CDL specification exists? what is it for? IMHO, now we have the WSDL as a contract to define the service in a language-independent way.  we can consider the "interface" as a contract definition in the JAVA world. But we don't have any thing to define the collaboration contract among multiple participants yet. Some people might say the UML Sequence diagram is a way to document it, but it lacks of the data description which has been used in the exchanges in the collaboration.

With the WS-CDL spec and its according tool, it can help us to design a system from top-down approach, well, it is sort of reminding me the era of MDA(Model Driven Architecture), personally, I am not a fan of MDA, that includes a lot of code generation. To some extent, WS-CDL is belong to the MDA, but as I said before, WS-CDL just defines the contract that multiple participants are working, it is not trying to describe everything in detail, so that you can build the whole system with one "Generate Code" click.

WS-CDL is mainly used for the Business Analyst. With current tools support, it can generate to WS-BPEL or Java skeleton code.

So, back to the WS-CDL specification itself, what is it composed of?

1. Collaborating Participants



	
  * 1.1 RoleType   -- It defines the role, as the minimum unit for participants.

	
  * 1.2 RelationshipType -- It defines the relationship in roles.

	
  * 1.3 ParticipantType -- It is consist of one or multiple roles.

	
  * 1.4 ChannelType -- How and where participants collaborate.


2. Information Driven Collaborations

	
  * 2.1 InformationType -- described the type of information used, simple wrapper for xsd.

	
  * 2.2 Variable

	
  * 2.3 Expressions

	
  * 2.4 Token and TokenLocator. (Tokens differ from variables in that variables contain values which MAY be populated as the result of actions or events within a choreography life-line whereas tokens contain information that define the piece of the data that is relevant.)

	
  * 2.5 WorkUnit

	
  * 2.6 Choreography

	
  * 2.7 Choreography Life-line

	
  * 2.8 Choreography Exception Handling

	
  * 2.9 Choreography Finalization


3. Activities

3.1 Ordering Structures

	
  * 3.1.1 Sequence

	
  * 3.1.2 Parallel

	
  * 3.1.3 Choice


3.2 Interacting

	
  * 3.2.1 Interaction Based Information Alignment.


For full and detailed explanation please see [WS-CDL specification.](http://www.w3.org/TR/ws-cdl-10/)

Also, see [Gregor's Presentation ](http://www.infoq.com/presentations/hohpe-soa-conversations) at infoQ.
