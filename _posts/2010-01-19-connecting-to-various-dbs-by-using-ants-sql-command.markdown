---
date: '2010-01-19 17:12:00'
layout: post
slug: connecting-to-various-dbs-by-using-ants-sql-command
status: publish
title: Connecting to various DBs by using ant's sql command.
wordpress_id: '267'
categories:
- Database
---

As you see from [my previous blog](http://jeff.familyyu.net/2010/01/using-oracle-instant-and-sqlplus-in.html), I set up oracle client to connect to the remote DB server to do the debug. If you just deal with one DB server, this should be fine, what if you need to test against various DB servers, like mysql, postgres, oracle and sqlserver, which is [our riftsaw project](http://jboss.org/riftsaw) need to be tested against, so instead of installing all of these clients, I am using the [Apache Ant's sql command](http://ant.apache.org/manual/).

I added a command to show all of tables in the db, below is the build.xml that I used.
[xml]
 <target name="db.show.tables"
             depends="log.properties, copy.ojdbc"
             description="show tables in db">
   <sql driver="${driver}"
        url="${connection.url}"
        userid="${username}"
        password="${password}"
        onerror="continue"
        print="true">
     ${show.table.sql}
     <classpath>
       <fileset dir="drivers">
           <include name="*.jar"/>
       </fileset>
     </classpath>
   </sql>
   </target>
[/xml]
Different database vendor has its own syntax for showing tables, as I defined below.
[xml]
<condition property="show.table.sql" value="show tables;">
       <equals arg1="${database}" arg2="mysql" />
 </condition>
 

 <condition property="show.table.sql" value="select table_name from information_schema.tables where table_schema='public' and table_type='BASE TABLE';">
       <equals arg1="${database}" arg2="postgres" />
 </condition>

 <condition property="show.table.sql" value="select table_name from tabs;">
       <equals arg1="${database}" arg2="oracle" />
 </condition>

 <condition property="show.table.sql" value="select name from riftsaw..sysobjects where xtype = 'U';">
       <equals arg1="${database}" arg2="sqlserver" />
 </condition>
[/xml]
By using this approach, you don't need to install those db clients, which could save you a lot of time.
