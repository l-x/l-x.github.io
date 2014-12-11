---
layout: post
title: "Create an empty branch with git"
date: 2014-12-11 10:49:20 +0100
comments: true
categories: 
- git
- github
---

Sometimes you need to create an emtpy branch, especially for [GitHub's][github] [project pages](https://help.github.com/articles/user-organization-and-project-pages/#project-pages). Below you will find the most simple solutin I've found so far.
<!--more-->

``` sh
$ git checkout --orphan gh-pages # create orphan branch
Switched to a new branch 'gh-pages'

$ git branch # make sure not to be in any branch
  master

$ git reset --hard HEAD # reset working tree

$ git commit --allow-empty -m "initial empty commit" # create empty commit, best practice
[gh-pages (root-commit) b00b135] initial empty commit

$ git branch # check if the new branch was created
* gh-pages
  master
```