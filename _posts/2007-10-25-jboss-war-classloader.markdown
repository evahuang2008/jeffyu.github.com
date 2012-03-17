---
date: '2007-10-25 21:52:00'
layout: post
slug: jboss-war-classloader
status: publish
title: JBoss war classloader
wordpress_id: '161'
categories:
- Java
---

(Note: below only has been tested against JBoss4.0.5 and JBoss4.2)

By default, when you deploy a war file to JBoss, it uses the "child-first" and "tomcat" classloader, which is not as same as JBoss's classloader.

If you want to change it to use the JBoss's classloader, Need to update the "jboss-service.xml" in the $JBoss_HOME/server/default/deploy/jbossweb-tomcat55.sar/META-INF folder (for JBoss4.0.5). This file located in the $JBoss_HOME/server/default/deploy/jboss-web.deployer/META-INF folder for JBoss4.2.1.

There are two options in the jboss-service.xml:
[xml]
<attribute name="Java2ClassLoadingCompliance">false</attribute>
<attribute name="UseJBossWebLoader">false</attribute>
[/xml]
Above is the value by default.
