---
layout: post
title:  "Remove history from github"
categories: Miscellaneous
tags:  git
excerpt: null
mathjax: true
author: Bo Chen
---

* content
{:toc}

In order to delete the history of the git commit and make it the branch new repo, please follow the steps below

* Checkout the code to a new branch  
  `git checkout --orphan latest_branch`

* Stage the code  
  `git add -A`

* Commit the change  
  `git commit -am "commit message"`

* Delete the master branch  
  `git branch -D master`

* Rename the current branch to master  
  `git branch -m master`

* Push to remote branch  
  `git push -f origin master`