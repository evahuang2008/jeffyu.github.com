---
date: '2007-06-30 06:59:22'
layout: post
slug: database-setup-tips
status: publish
title: Database setup Tips
wordpress_id: '27'
categories:
- Chinese
- Others
---

前两周写的..... 

• Oracle 817 can not be set up using domain account, you'd better use the administrator account for local machine.
• Once the error shows " Shared memory realm doesn't exist", it means Oracle HTTP service doesn't work right.
• If you find "java error" in Oracle 817, it means the JDK in apache folder is out-of-date, you need to download the latest JDK and replace that folder, and then, if it is possible, you need to recreate the database that you've already existed.
• If you want to install SQL Server 2000, and found they are some errors in it, most of situation, what you need to do is to setup the SQL Server database Patch.
• Install Oracle10g, after finished the database setup. Add a listener if it doesn't exist; Add a new database, and then Add a local net service through network assistant.


