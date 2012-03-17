---
date: '2008-10-06 16:52:00'
layout: post
slug: hibernate-annotation-of-map
status: publish
title: Hibernate annotation of Map
wordpress_id: '219'
categories:
- Java
- JBoss
tags:
- Hibernate
- JPA
---

If you happen to have a simple Map<String, String> to be mapped by using Hibernate annotation, and don't want to create an object by using List, such as List<Property>, the property contains the key and value member. Then you can use the Hibernate Annotation, "CollectionOfElements", it is hibernate specific, not JPA-specific. Details please refer to [this blog entry](http://i-proving.ca/space/Technologies/Hibernate/Hibernate+Annotation+Examples/Collection+of+Elements), it is well documented.
