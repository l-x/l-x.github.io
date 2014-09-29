---
layout: post
title: "Messing around with PHP's late static binding"
date: 2014-09-29 14:39:58 +0200
comments: true
share: true
categories: 
    - php
    - snippets
    - late static binding
---

Some weird PHP behavior I stumbled over while debugging our software. This is known at least since 2009 (https://bugs.php.net/bug.php?id=50031). Maybe this opens a few new possibilities for dependency injection or nasty hacks.
<!--more-->
{% gist:08e14a5060495add5842 %}