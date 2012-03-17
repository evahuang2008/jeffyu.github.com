---
date: '2007-09-22 04:31:00'
layout: post
slug: create-a-simple-ejb2-sample
status: publish
title: Create a simple EJB 2.x sample.
wordpress_id: '152'
categories:
- Java
---

Although I have been developing EJB for almost two years, I havent spent time in investigating the EJB infrastructure, especially in this EJB-anti era.
Since now I am working on the JCA1.5 stuff, need to pick up the EJB stuff again, and this is a good chance for me to investigate EJB a little more.

1. RemoteObject
[java]
public interface GreeterRemote extends EJBObject {
String greetMe(String user) throws RemoteException;
}
[/java]
2. HomeObject
[java]
public interface GreeterHome extends EJBHome {
GreeterHome create() throws RemoteException, CreateException;
}
[/java]
3. BusinessImpl (SessionBean)
[java]
public class GreeterBean implements SessionBean {

private SessionContext sessionContext;

public void ejbActivate() throws EJBException, RemoteException {
}

public void ejbPassivate() throws EJBException, RemoteException {
}

public void ejbRemove() throws EJBException, RemoteException {
}

public void setSessionContext(SessionContext context) throws EJBException, RemoteException {
this.sessionContext = context;
}

/**
* Implement business method.
*/
public String greetMe(String user) throws EJBException, RemoteException {
return "From Server, greetMe by [" + user + "]";
}
}
[/java]
4. ejb-jar.xml

5. jboss-ejb-jar.xml (vendor-specific xml config)

6. Package the files, and deploy it to container.
The jar structure would be:
|---META-INF
|-----------/ejb-jar.xml
|-----------/jboss-ejb-jar.xml
|----java
|--------/GreeterRemote.class
|--------/GreeterHome.class
|--------/GreeterBean.class
