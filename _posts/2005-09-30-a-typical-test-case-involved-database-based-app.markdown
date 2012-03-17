---
date: '2005-09-30 01:37:48'
layout: post
slug: a-typical-test-case-involved-database-based-app
status: publish
title: A typical test case involved database based app
wordpress_id: '96'
categories:
- Java
---




Posted by: [_Jakob Jenkov_](http://spaces.msn.com/user/userthreads.tss?user_id=304680) on September 28, 2005  
  
Hi Jeff, the situation you describe is a typical situation when testing database based applications. Here is what I normally do:  
  
public void testDbStuff() throws Exception {  
  
   Connection connection = null;  
   try{  
      connection = openConnection();  
      connection.setAutoCommit(false);  
      //in a method if I need it again in a later test case.  
      doInsertStuff();   
  
   } finally {  
      if(connection != null){  
         connection.rollback(); //deletes all inserts and updates and deletes etc. done during test.  
         connection.close();  
      }  
   }  
}  
  
  
Notice how the transaction is rolled back in the finally clause. That way you don't have to worry about what updates you made in the database during the test. It is all deleted and set back, after the test. The nice thing about that is, that if your database contains other test data, for instance for playing around with when testing the UI, these test data will NOT be erased or changed by the test.  
  
Sometimes I create the connection and call setAutoCommit(false) in the setUp() method of the test class, and call connection.rollback(); and connection.close(); in the tearDown() method. However, I have experienced that if an exception is thrown from the test method, the tearDown method is not always called. So, usually I use the try-finally method. 
