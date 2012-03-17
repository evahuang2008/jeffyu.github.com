---
date: '2007-11-07 17:08:00'
layout: post
slug: a-little-thinking-on-rest
status: publish
title: A little thinking on REST
wordpress_id: '165'
categories:
- Java
- REST
---

[REST](http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm) is becoming a buzzword now, a lot of people are adopting REST, building RESTful services, especially for Dynamic Language, Ruby On Rails application is an obvious example on this.  
  
However, I am thinking that for Java, it still needs some time to move to RESTful Service, or there are still some issues that RESTful services need to solve, or needs some time to take.  
  
1. Now, we can expose services RESTful way, but due to the data format is not defined, you can use any kind of data format if you want. So you need to use your own parser to parse the data to Java Object. (Using Java as an implementation language for example). Yeah, I know we can used the 3rd data binding library, such as JAXB, Xmlbean etc, but we still need to define our own xml schema for data exchange.  
  
I think why the HTTP succeed is that it has a Engine(Internet Explore) that can consume the Resources. For HTTP, it always return the resources as HTML format, which can consumed by Internet Explore. Now, every one has that engine, so it is not a problem.  
  
Yes, RESTful web services do not have the operation concept, but its data still have not been defined yet. Someone said constraints leads to the simplicity... [Atom](http://atompub.org/) seems to define data format. So that we can get data in a uniform way too.  
  
2. Resource-Oriented versus Service-Oriented development, this is a mind change stuff, and I guess it needs some time for developers to change their mind and adopt it.  
  
3. I am not sure that from now on, developers are all concern about Resources, in their mind, there are no databases, no files, all of them are Resources... say, there might be not using ORM tool, since now developers are all operating the object stuff, and all other data are exposed in RESTful way..  
  
4. Security stuff, using HTTPS do the authentication sometimes is too heavy...  
  
Very Interesting...
