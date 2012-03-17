---
date: '2008-07-13 04:07:00'
layout: post
slug: log4j-configuration-in-jboss-as
status: publish
title: Log4j configuration in JBoss AS.
wordpress_id: '208'
categories:
- Java
- JBoss
---

Yeah, log4j configuration is easy, but sometimes you might find it is a little bit hard for you to configure it in JBoss AS if you are new to it. So following is the step-by-step example which I was used in [overlord](http://jboss.org/soag/) [cdl](http://jboss.org/soag/cdl/index.html) project.

open up the jboss-log4j.xml in the $JBossAS/server/domain(ie. default)/conf folder.

1. the jboss-log4j.xml default for
is "DEBUG", in my case, I want to change it to "INFO" level, since the "DEBUG" level is too verbose.
[xml]
<root>
<value="INFO">
<ref="CONSOLE">
<ref="FILE">
</root >
[/xml]
2. Add your own package log level to DEBUG: like
[xml]
<category>
<name="org.jboss.soa.overlord">
<value="DEBUG">
</category>
[/xml]
3. If you want to show the DEBUG level to the console, you also need to update the 'Threshold' level to 'DEBUG' in CONSOLE appender.
[xml]
< name="Threshold" value="DEBUG">
[/xml]
Yeah, that's all, quite easy, restart your sever, you would see it take effect. If you want to know more about JBossLog4j, you can refer to [this document](http://docs.jboss.org/jbossas/AllDocsSubscription/JBossLog4j.pdf), which was written by Scott Stark.

[update Dec 2, 2009] A more convenient way for you to do the debug would be add a 'appender', and then direct ur log into that appender. like following:
[xml]
<appender name="RS" class="org.jboss.logging.appender.RollingFileAppender">
<errorHandler class="org.jboss.logging.util.OnlyOnceErrorHandler"/>
<param name="File" value="${jboss.server.log.dir}/riftsaw.log"/>
<param name="Append" value="true"/>
<param name="MaxFileSize" value="500KB"/>
<param name="MaxBackupIndex" value="1"/>
<param name="Threshold" value="DEBUG"/>

<layout class="org.apache.log4j.PatternLayout">
<param name="ConversionPattern" value="%d %-5p [%c] %m%n"/>
</layout>
</appender>

<category name="org.apache.ode">
<priority value="DEBUG" />
<appender-ref ref="RS" />
</category>

<category name="org.jboss.soa.bpel">
<priority value="DEBUG" />
<appender-ref ref="RS" />
</category>
[/xml]
Note: I am validating this against JBossAS4.2.2GA.
