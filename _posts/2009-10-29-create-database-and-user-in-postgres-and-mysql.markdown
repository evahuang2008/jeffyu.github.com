---
date: '2009-10-29 16:32:00'
layout: post
slug: create-database-and-user-in-postgres-and-mysql
status: publish
title: Create Database and user in Postgres and Mysql.
wordpress_id: '259'
categories:
- Database
---

Since I worked in SOA area, haven't touched the database for couple years, although in some projects, I need to test against various database (Mysql, Postgres, Oracle etc), but it is very basic stuff, like create database, users etc.

This post basically is a memo for me, I need to work with various DBs from time to time, and think it is best to record it in my blog, instead of looking into the manual again. ;-). Also, you could see this is a follow-up post for my previous [postgres installation blog](http://jeff.familyyu.net/2008/05/postgresql-installationconnection-in.html).

1. **Postgres**

1) connect Postgres


> psql -h localhost -U postgres


2) add user


> create user jeff with password 'jeff'


3) create database


> create database jeffdb


4) grant db to user


> grant all privileges on database jeffdb to jeff


Log out with "q" command

Log in jeffdb through user jeff:


> psql -d jeffdb -U jeff


2. **Mysql**

1) connect mysql


> mysql -u root -p 'urpassword'


2) create database


> create database jeffdb


3) allow user jeff to connect to the server from localhost using the password jeff


> grant usage on *.* to jeff@localhost identified by 'jeff';


4)grant all privileges on the jeffdb database to this user


> grant all privileges on jeffdb.* to jeff@localhost ;


Log out and log in through jeff user.


> mysql -u jeff -p'jeff' jeffdb


[Reference]
1. [How to add postgres user and create db](http://www.cyberciti.biz/faq/howto-add-postgresql-user-account/)
2. [Create mysql database and set privileges into a user](http://www.debuntu.org/how-to-create-a-mysql-database-and-set-privileges-to-a-user)
