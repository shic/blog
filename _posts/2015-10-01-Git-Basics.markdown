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




# Merge

### [Merge a git branch into master](https://stackoverflow.com/questions/5601931/best-and-safest-way-to-merge-a-git-branch-into-master)

```
git checkout master
git pull origin master
git merge name_of_branch_to_merge
```

### Make a branch as master branch

```
git checkout master
git checkout -b name_of_copy_of_master_branch //make a copy of master branch
git checkout master
git reset --hard b8c3(form which commit created the branch)
git merge name_of_branch_to_merge
git branch -d name_of_branch_to_merge
```

### 

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






# Search Commit

## Method 1:

1. https://github.com/search
2. Insert user/repo and content to look for `user:shic repo:react-boilerplate-2017 table`



## Method 2:

```
git log -g -i --grep='Table'
```



```
git log --all --oneline | grep -i "Table"
```

-i: ignore case

' ' or " " both works



# Git log

```
git reflog
```



# Bug detect

## Git checkout

```
git checkout {commit}
git chekout master //remember to checkout to master before any commit!!!
```



## Git bisect

```
git bisect start
git bisect bad # to indicate current commit is broken
git bisect good {commit} # to indicate the last good commit
git bisect bad|good # you'll run this command over and over while Git changes commits to find which commit introduced the bug
git bisect reset # to bail out of everything and move back to original HEAD (i.e. the latest broken commit)
```

You can also filter what commits are included in a bisect like so:

```
git bisect start -- ./sub_directory
```

This will mean only commits that affected files inside of `./sub_directory` are considered.

> Note: you can also specify a range of commits to skip: `git bisect skip 0dae5f ff049ab ...`

[](https://gist.github.com/shic)



# [Create a branch from unstaged/uncommitted changes](https://stackoverflow.com/questions/2569459/git-create-a-branch-from-unstaged-uncommitted-changes-on-master)

```
git checkout -b new_branch_name
git add .
git commit -m "<Brief description of this commit>"
```