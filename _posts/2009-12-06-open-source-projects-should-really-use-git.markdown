---
date: '2009-12-06 02:05:00'
layout: post
slug: open-source-projects-should-really-use-git
status: publish
title: open source projects should really use Git
wordpress_id: '262'
categories:
- SCM
tags:
- Git
---

I am starting to work on one task in ODE, titled cleanup JPA impl ([https://issues.apache.org/jira/browse/ODE-704](https://issues.apache.org/jira/browse/ODE-704)), basically it is a quite large refactoring on DAO layer of ODE project. Because I am not a ODE committer, It is not an easy job to get this task done.

After talked with [Rafal Rusin](http://rrusin.blogspot.com/) on the ode IRC channel, he suggested that I create a git project in [github](http://www.github.com/), which clones the ode git repo, and then put my jpa refactoring experiment branch in github, once my code has finished, and passed all the tests, they can merge my branch into the ode trunk.

I've heard of [Git](http://git-scm.com/) for a while, but didn't get a chance to use it, as currently I am still using the Subversion as SCM repository. One thing that I learnt from history is that try to avoid using branch in SVN or CVS as much as possible, it is really a headache for merging branch back to trunk, so this is very inconvenient for you to try some new feature, or some experiment codes.

Create a project at Github is very easy, if you have problems, [GitHub's help](http://help.github.com/) is your friend. I have to say that Github did an awesome job on project hosting, it makes you very easy to browse your code, the diff message between version etc.

Watching the [Linus' Git talk on Google Tech conf](http://www.youtube.com/watch?v=4XpnKHJAok8), very interesting, totally agreed that one pain with centralized repository like CVS or SVN, is that you need to get the commit access for your contribution (I am not saying a small fix, or patch, I meant some large task, or feature etc, which would require multiple patches, and might take one or two weeks), like the case that I am hitting now. Alternatively, if you are hosting code repository by using Git, I can clone it from the url, and pull the changes into my local workspace to make it up-to-date, and then push it into some other repository, once I've finished my task, I will send you my code repository, and then you can take a look at those code to decide if you want to accept my code or not. In this case, I don't need to have a commit permission in advance. Also merge in Git is very easy, it makes collaboration really easy.

So, I would strongly recommend that every open source project should embrace the Git as scm tool, lets forget about Subversion, CVS. Lets embrace the branch. ;-)

couple resources that could help you get started with Git.
1. [Git website](http://git-scm.com/)
2. [GitHub webiste](http://www.github.com/)
3. [Learn Git website](http://learn.github.com/) (Strongly recommend for learning)
