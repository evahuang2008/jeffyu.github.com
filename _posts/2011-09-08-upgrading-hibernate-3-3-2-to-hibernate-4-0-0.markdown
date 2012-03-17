---
date: '2011-09-08 19:48:48'
layout: post
slug: upgrading-hibernate-3-3-2-to-hibernate-4-0-0
status: publish
title: Upgrading Hibernate 3.3.2 to Hibernate 4.0.0
wordpress_id: '699'
categories:
- Java
- JBoss
tags:
- Hibernate
- RiftSaw
---

As you may know, [JBoss AS 7](http://www.jboss.org/jbossas) is incredible fast and low-memory, and it comes with Hibernate 4.0.0 by default. Since AS 7.0.1, it is easy for you to support both Hibernate 3.x  and Hibernate 4.0.0 under JBoss AS, thanks to the modular classpath here. If you want to run Hibernate 3.x under AS7 along with Hibernate 4, you should check out [this blog entry ](http://in.relation.to/Bloggers/UsingADifferentPersistenceProviderWithAS701)and [this documentation](https://docs.jboss.org/author/display/AS7/JPA+Reference+Guide).

In [RiftSaw 3](https://github.com/riftsaw) development, we are taking this opportunity to upgrading its JPA layer from JPA 1.0 to JPA 2.0, as JPA 2.0 is back compatible, it shouldn't be an big issue. However, we've implemented the [ConnectionProvider](http://www.docjar.com/html/api/org/hibernate/connection/ConnectionProvider.java.html) and [TransactionManagerLookup](http://www.docjar.com/html/api/org/hibernate/transaction/TransactionManagerLookup.java.html) interfaces, since we've created the Datasource and TransactionManager on our own, we need to implement these two interfaces to ask Hibernate to use our own one.

In Hibernate 4.x, the whole package has been split into three categories, API/Impl/SPI.  So the ConnectionProvider class has been re-packaged at: **org.hibernate.service.jdbc.connections.spi.ConnectionProvider**, if you see the [internal implementation](http://grepcode.com/file/repo1.maven.org/maven2/org.hibernate/hibernate-core/4.0.0.Beta3/org/hibernate/service/jta/platform/internal/JBossAppServerJtaPlatform.java) of this, you would also notice that it also implements the [Configurable](http://grepcode.com/file/repository.jboss.org/nexus/content/repositories/releases/org.hibernate/hibernate-core/4.0.0.Alpha2/org/hibernate/service/spi/Configurable.java) and [Stoppable](http://grepcode.com/file/repository.jboss.org/nexus/content/repositories/releases/org.hibernate/hibernate-core/4.0.0.Alpha2/org/hibernate/service/spi/Stoppable.java?av=f). The Configurable interface allows you to access to the Hibernate's properties, which is kept as Map. It is much like Spring's BeanNameAware interface, where you get to access to the BeanName. So below is the code snippet that I used for my ConnectionProvider.

[java]
public class DataSourceConnectionProvider implements ConnectionProvider, Configurable, Stoppable  {

  private Properties _props;

  private boolean available = true;

  public DataSourceConnectionProvider() {
  }

  @SuppressWarnings( {"unchecked"})
  public void configure(Map properties) {
	 _props = new Properties();
	 _props.putAll(properties);
  }

  public Connection getConnection() throws SQLException {
	if (!available) {
		throw new HibernateException( "Provider is closed!" );
	}
    Connection c = HibernateUtil.getConnection(_props);
    DbIsolation.setIsolationLevel(c);
    return c;
  }

  public void closeConnection(Connection con) throws SQLException {
    con.close();
  }

  public boolean supportsAggressiveRelease() {
    return true;
  }

  public boolean isUnwrappableAs(Class unwrapType) {
		return ConnectionProvider.class.equals(unwrapType) ||
				DataSourceConnectionProvider.class.isAssignableFrom(unwrapType);
  }

  @SuppressWarnings( {"unchecked"})
  public  T unwrap(Class unwrapType) {
		if (ConnectionProvider.class.equals(unwrapType) ||
				DataSourceConnectionProvider.class.isAssignableFrom(unwrapType)) {
			return (T) this;
		} else {
			throw new UnknownUnwrapTypeException( unwrapType );
		}
  }

  public void stop() {
	available = false;
  }
}
[/java]

For the TransactionManagerLookup interface, you would get WARN  saying this API has been deprecated ( I believe it has been deprecated before 4.x, but I didn't get a chance to upgrade it until now), we should implement the **org.hibernate.service.jta.platform.spi.JtaPlatform **SPI instead, and set it to the 'hibernate.transaction.jta.platform' property. Instead of having a class that implement the JtaPlatform SPI directly, I've subclassed it from the  [AbstractJtaPlatform](http://grepcode.com/file/repo1.maven.org/maven2/org.hibernate/hibernate-core/4.0.0.Beta5/org/hibernate/service/jta/platform/internal/AbstractJtaPlatform.java#AbstractJtaPlatform) class, so that I've only needed to override two interfaces. Below is the code snippet for my custom JtaPlatform impl.

[java]/**
 *
 * uses {@link HibernateUtil} to obtain the JTA {@link TransactionManager} object.
 *
 * @author Jeff Yu
 *
 */
public class OdeJtaPlatform extends AbstractJtaPlatform {

	private Properties properties = new Properties();

	public void configure(Map configValues) {
		super.configure(configValues);
		properties.putAll(configValues);
	}

	@Override
	protected TransactionManager locateTransactionManager() {
		return HibernateUtil.getTransactionManager(properties);
	}

	@Override
	protected UserTransaction locateUserTransaction() {
		throw new UnsupportedOperationException("locateUserTransaction is not supported. Use the locateTransactionManager instead.");
	}

} [/java]

And then when you create your entityManagerFactory, remember to pass the following properties in.

[java]props.put(Environment.CONNECTION_PROVIDER, DataSourceConnectionProvider.class.getName());
props.put(Environment.JTA_PLATFORM, OdeJtaPlatform.class.getName());[/java]

Done, the custom ConnectionProvider and JtaPlatform implementation should be all set now.

Hope this will help you do the Hibernate upgrade at some point. Here, I'd like to thanks [Strong Liu](http://in.relation.to/Bloggers/StrongLiu) to send the helpful links to me on this upgrading. :-)
