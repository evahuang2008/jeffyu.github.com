---
date: '2008-07-20 06:20:00'
layout: post
slug: deploying-opensso-running-its-samples-in-jbossas
status: publish
title: Deploying OpenSSO & Running its samples in JBossAS
wordpress_id: '210'
categories:
- Java
- JBoss
tags:
- OpenSSO
---

It is a little bit tricky for me to get installed the OpenSSO against JBossAS4.x, So here I'd like to describe the steps that I am doing, if others new to opensso, hopefully it might be helpful for them.

Deploying opensso in the JBossAS

1. Download the opensso build 4.5 zip from the [opensso download page](https://opensso.dev.java.net/public/use/index.html). (I validated build4 and 4.5 against JBossAS4.2.2.GA)

2. Following the [release note](http://download.java.net/general/opensso/stable/openssov1-build4/B4-ReleaseNotes.html) of deploying the opensso.war in the JBossAS4.x.

3. You will also need to increase the Permsize in $JBoss/bin/run.conf by adding following option in the JAVA_OPTS line.


> -XX:MaxPermSize=512m in the


4. Then start the $JBoss/bin/run.sh, you should be able to access its admin page in http://yourdomain:8080/opensso. (OpenSSO doesn't work well with the localhost, so you should specify a full qualified domain for it)

5. And then you can have a default configuration from http://yourdomain:8080/opensso link.

6. After you have the default configuration, you should be able to login the system by using: amAdmin, amLdapuser and with the password that you set before.

OK, so above the steps to deploy the opensso.war, not much tricky here. And then, I am going to run an example that based on opensso sdk. (openssoclientsdk.jar).

Running the example:

In the opensso directory that you extracted from the opensso.zip, you can see a sub-folder is: samples.

1) Go to the $samples, you will see the fam-client.zip. (Because sun's commercial product name is Federation Acess Manager, that is what the fam stands for.)
2) Unzip that fam-client.zip, you will see it contains sdk and war folders
3) Go to the sdk folder. run the 'chmod 755 scripts/*.sh' to make the script runnable.
4) run: 'scripts/compile-samples.sh' to build the sample code.
5) run: 'scripts/setup.sh', (This is to configure the AMConfig.properties.)


> Debug directory (make sure this directory exists): /var/local/tmp (This can be other places)
Password of the server application: opensso1 (Not sure this one, I just input a random one.)
Protocol of the server: http
Host name of the server: putian.nay.redhat.com
Port of the server: 8080
Server's deployment URI: opensso
Naming URL (hit enter to accept default value, http://putian.nay.redhat.com:8080/opensso/namingservice):


6) run: "scripts/Login.sh", you will see:


> Realm (e.g. /): opensso
Login module name (e.g. DataStore or LDAP): DataStore
Login locale (e.g. en_US or fr_FR): en_US
DataStore: Obtained login context
User Name:amAdmin
Password:


Input your password, it should show you like following:


> Login succeeded.
Logged Out!!


Well, this example shows you how to do the authentication by using openssoclientsdk.jar.

Note: I am validating opensso build4 and 4.5 against JBossAS4.2.2.GA. If you have deployed the opensso.war in the JBossESB server, it has a known issue at https://jira.jboss.org/jira/browse/SOA-731
