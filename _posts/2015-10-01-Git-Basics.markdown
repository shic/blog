---
layout:     post
title:      "Git Basics"
subtitle:   "Some useful command lines"
date:       2015-10-01 12:00:00
author:     "Shi"
---



# Git commit 

1. `git add .` to add your changes to git 
2. `git commit -m "commit msg"`





# Fetch and Rebase remote version 

1. Before fetch remote repo, be sure you have already committed your changes 
2. `git fetch`
3. `git rebase origin/master` (Put the name of your branch)
4. Resolve conflict if there are
5. `git add . `
6. `git rebase --continue`



