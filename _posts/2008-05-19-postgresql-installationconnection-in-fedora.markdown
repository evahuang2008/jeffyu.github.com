---
date: '2008-05-19 20:14:00'
layout: post
slug: postgresql-installationconnection-in-fedora
status: publish
title: Postgresql installation/connection in Fedora
wordpress_id: '203'
categories:
- Database
- OS
tags:
- Fedora
- Postgresql
---

Because I wan to try the [JON 2.0](http://www.jboss.com/products/jbosson), I gotta have a database, currently the JON supports two databases, Postgres and Oracle. So here I choose the Postgres as it is open source.

I am using the Fedora8, so install the postgres just simply need to run


> yum install postgresql-server


After I installed the postgres, I created it with following command:


> service postgresql initdb
service postgresql start


And then I try to (as reference[1] described)


> createuser -h 127.0.0.1 -p 5432 -U postgres -S -D -R rhqadmin


it tells me that " FATAL:  Ident authentication failed for user "postgres". This error mostly means you need to update the "pg_hba.conf" file.

try to run


> ps aux | grep postmaster


to find out where the "pg_hba.conf" located. (Here thanks to illya77 and pilhuhn in #rhq at irc.freenode.net help me solve this problem).

Update the pg_hba.conf  suggested, and then

Edit the postgres host based access configuration file (pg_hba.conf), which typically would be at: /var/lib/pgsql/data/pg_hba.conf

Modify the local line to use "trust" based authentication rather than "identity". Please review the PostgreSQL documentation before making this change and take the security

    
    local all  all   trust


After that, restart the postgresql to make the change taking effect.


> service postgresql restart


At last: run


> psql -h localhost -U postgres


to see if it can log in.

[Reference]
1. [ Postgres Quick Start Installation](https://docs.jbosson.redhat.com/confluence/display/JON2/Postgres+Quick+Start+Installation+Guide)
