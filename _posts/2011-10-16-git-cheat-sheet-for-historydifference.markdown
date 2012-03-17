---
date: '2011-10-16 14:46:33'
layout: post
slug: git-cheat-sheet-for-historydifference
status: publish
title: Git Cheat Sheet for history/difference.
wordpress_id: '731'
categories:
- SCM
tags:
- Git
---

I knew it has some good [Git Cheat Sheets](http://help.github.com/git-cheat-sheets/) on the internet. So I won't try to create yet another Git Cheat Sheet. Instead, I'll focus on some commands for the history and file difference, as I often use them to check what has been updated on the commits, and what files been changed in there etc. Usually I went to GitHub to check out the previous commits, as it did a very good job on showing the updated files, difference on each file etc. However, at some time, my home internet is very slow, so it could be painful to go to the Github to check on those commits. (It is nothing wrong in Github, it is just in my particular case at some time due to bad network).

Git is a DVCS, so it means that we have all histories, logs in my local machine, the remote one should be served as a backup/collaborate purpose. So it means for checking the commits/difference, it should be accomplished without connecting to internet.  Here I'll try to enumerate some options/commands that I ran for checking those updates/commits. If you have any other good usages/commands that I left out. please feel free to make a comment.

1. Show all of previous commits (result only shows commit summary):


> git  log


2. Show the latest n commits:


> git  log  -n


3. Show the statistics (like updated file list) in previous commits:


> git log --stat


4. Show previous commits with patches:


> git log -p


5. Show a specific commit with commit hash id, you just need to have enough first couple letters to make it unique:
Add --stats (if you want to show the statistics) and -p (if you want to show the detailed diff) options.


> git show 36b314c (first couple letters of id)


6. Show commits/histories to a specific file (-p, -n apply here as well, but should be in front of filepath):


> git log -- filepath


7. Show a diff on a specific file with a specific commit:


> git show commitId (like 36b314c for example) -- filepath


9. Show difference between two commits:


> git diff firstCommitId secondCommitId


10. Show difference between two commits for a specific file.
 

> git diff firstCommitId secondCommitId -- filepath




