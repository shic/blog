---
layout:     post
title:      "Git Basics"
subtitle:   "Some useful command lines"
date:       2015-10-01 12:00:00
author:     "Shi"
---



## Personal access tokens

[Generate new token](https://github.com/settings/tokens/new)

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




# Duplicating a repository

1. Create a bare clone of the repository.

   ```
   git clone --bare https://github.com/exampleuser/old-repository.git
   ```
   Got temporary local repository repo `old-repository.git`



2. Mirror-push to the new repository.
   ```
   cd old-repository.git
   git push --mirror https://github.com/exampleuser/new-repository.git
   ```

3. Remove the temporary local repository you created 

