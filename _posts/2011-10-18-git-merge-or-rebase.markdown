--- 
layout: post
title: Git merge or rebase?
published: true
tags: 
- Git
- SCM
type: post
status: publish
---
There are many posts about the difference on git's rebase and merge commands, here I'd like to link two of them that I think did a great job on the explanation.

1. [Rebase vs Merge in Git](http://gitguru.com/2009/02/03/rebase-v-merge-in-git/)
2. [Avoid Merge commit in Git](http://www.kerrybuckley.org/2008/06/18/avoiding-merge-commits-in-git/), this one shows very detail about the difference on these two options, and it is the exact problem I was facing.

I'd also like to quote the work pattern that is described in the above 1st link. (The result is basically put all your branch work/commits ahead of your base branch, for example master, and of course without adding those meaningless merge commits that you would have if you use the git merge.)

> 1. Create new branch B from existing branch A
> 2. Add/commit changes on branch B
> 3. Rebase updates from branch A
> 4. Merge changes from branch B onto branch A


I typically use the 'master' branch as the base branch, which means that I only sync this branch from the remote repository, and only merge commits into this branch when I think the bug/feature is completed. Once I've  done the merge in master, I'll do the commit and push, so the code in master branch's staging repository is very short. However, I've done a lot of pull request from remote repository into the master branch, as I need to sync other people's work, and then I'll do the rebase on the topic/bugfix branch that I am working on to sync the work without adding the merge commit, and put my commit in front of others commits that are already in the repo.

One caution with regard to the rebase operation is: (Again quote from the 2nd link that I pointed)
> If you've shared the branch with anyone else, or are pushing it to a clone of the repository, do not rebase, but use merge instead. 

From the man page:
> When you rebase a branch, you are changing its history in a way that will cause problems for anyone who already has a copy of the branch in their repository and tries to pull updates from you. You should understand the implications of using git rebase on a repository that you share.

