---
date: '2006-05-23 02:39:02'
layout: post
slug: tdd-%e5%85%b8%e5%9e%8b%e7%9a%84%e5%af%b9%e4%ba%8edao%e6%95%b0%e6%8d%ae%e6%b5%8b%e8%af%95%e7%9a%84test-cases
status: publish
title: TDD - 典型的对于DAO数据测试的Test Cases
wordpress_id: '56'
categories:
- Java
---

早上在TDD maillist中发现到Uncle Bob的一个mail: 特摘录如下:




  mbrown103 wrote:  
>  To give a simple example lets say I need to get data   
> from a database, using an inline sql string due to business rules, and   
> populate a dataset with it.  Now, I am sure that most of us can write   
> the code for this in just minutes.  I am just not sure how to approach   
> this in a TDD fashion.    
  
Test 1:  
   1. Make sure the database is empty.  
   2. Call the function that returns the dataset.  
   3. Make sure the dataset is empty.  
  
Test 2:  
   1. Make sure the database has one row, AND  
      that the row matches the query.  
   2. Call your function.  
   3. Make sure the dataset has one row.  
   4. Make sure the fields are correct.  
  
Test 3:  
   1. Make sure the database has one row, AND  
      that the row DOES NOT match the query.  
   2. Call your function.  
   3. Ensure the dataset is empty.  
  
Test 4:  
   1. Make sure the database has two rows, AND  
      that both rows match the query.  
   2. Call your function.  
   3. Make sure the dataset has two rows.  
   4. Make sure the fields are correct.  
  
Test 5:  
   1. Make sure the database has two rows, AND  
      that only one matches the query.  
   ...left to the reader as an exercize... 




 




没想到Test Case需要考虑到这么多种情况吧???
