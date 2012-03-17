---
date: '2008-08-04 19:02:00'
layout: post
slug: saving-serializable-object-by-using-hibernate
status: publish
title: Saving serializable object by using Hibernate
wordpress_id: '213'
categories:
- Java
- JBoss
tags:
- Hibernate
- JPA
---

Well, sometimes you might want to save the object as serializable into database, with the Hibernate, it is quite simply for you to do that.

1). Using @Lob annotation from hibernate-annotation library
2). Write the ObjectInputStream, ObjectOutputstream like following thread's code.([sebastian mitroi serializable java objects  in  mysql](http://blog.tremend.ro/2007/02/15/untitledserializable-java-objects-in-mysql/))
