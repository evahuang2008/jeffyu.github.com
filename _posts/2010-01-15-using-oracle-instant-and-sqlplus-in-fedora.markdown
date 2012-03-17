---
date: '2010-01-15 22:02:00'
layout: post
slug: using-oracle-instant-and-sqlplus-in-fedora
status: publish
title: Using Oracle Instant and Sqlplus in Fedora
wordpress_id: '266'
categories:
- Database
---

In case you are working against Oracle database, and don't want to install the whole Oracle DB mess, just want to use the sqlplus to connect to an existing db. Then see [this post](http://www.ioncannon.net/system-administration/114/using-oracle-instant-client-and-sqlplus/).  
  
I installed                           [oracle-instantclient11.2-basic-11.2.0.1.0-1.i386.rpm](http://download.oracle.com/otn/linux/instantclient/112010/oracle-instantclient11.2-basic-11.2.0.1.0-1.i386.rpm) and                          [oracle-instantclient11.2-sqlplus-11.2.0.1.0-1.i386.rpm](http://download.oracle.com/otn/linux/instantclient/112010/oracle-instantclient11.2-sqlplus-11.2.0.1.0-1.i386.rpm) in my box. (Fedora 10)  
  
Once you connect it successfully. simply run:  


> select table_name from tabs;  


to show the tables from your connected database.
