---
layout:     post
title:      "AngularDart"
date:       2016-03-13 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---
# AngularDart

# Guide

https://webdev.dartlang.org/angular/guide/component-styles

https://webdev.dartlang.org/angular/tutorial/toh-pt6



# **angular_components**

Official Example: https://github.com/dart-lang/angular_components/tree/master/examples

Lib: https://webdev.dartlang.org/api/angular/angular/NgClass-class



## Components

## Directive

ngClass: https://webdev.dartlang.org/api/angular/angular/NgClass-class



# Cheat Sheet

https://webdev.dartlang.org/angular/cheatsheet



# Debug

https://webdev.dartlang.org/guides/debugging



# Git hook

1. Create `pre-commit` file in `.git/hooks`

2. Remember to change the access permissions: ` chmod +x pre-commit`

3.  `pre-commit` file:

4. ```bash
    dart_files=$(git diff --cached --name-only --diff-filter=ACM | grep '.dart$')
    
    [ -z "$dart_files" ] && exit 0
    
    function checkfmt() {
      unformatted=$(dartfmt -n $dart_files)
      [ -z "$unformatted" ] && return 0
    
      echo >&2 "Dart files must be formatted with dartfmt. Please run:"
      for fn in $unformatted; do
        echo >&2 "  dartfmt -w $PWD/$fn"
      done
    
      return 1
    }
    
    checkfmt || fail=yes
    
    [ -z "$fail" ] || exit 1
    
    echo 'all okay?'
    
    exit 0
    ```



# Example Code

https://github.com/angular-examples/lottery