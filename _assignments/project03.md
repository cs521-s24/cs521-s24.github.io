---
layout: assignment
due: 2024-03-07 23:59:59 -0800
permalink: assignments/project03.html
title: Project03 - Elastic Array, File Stat
github_url: https://classroom.github.com/a/K1C_qhBi
published: true
---

## Requirements

### This is a short draft for 2/27 lecture. More examples and test cases to come
### Part 1

1. In C, arrays have fixed size, and are not dynamically resizable as in Python and Java
1. You will implement a resizable array in C, called `rarray`. The header file for rarray will be given in the inclass repo

### Part 2

1. Now that you have a resizable array, you can use it to traverse the filesystem and make a list of files, even if you don't know how many there are.
    ```text
    $ project03 /usr/include
    /usr/include
    /usr/include/python3.9
    /usr/include/python3.9/pyconfig-64.h
    /usr/include/openssl
    /usr/include/openssl/md5.h
    /usr/include/openssl/aes.h
    /usr/include/openssl/mdc2.h
    /usr/include/openssl/asn1.h
    /usr/include/openssl/modes.h
    ```
1. Options
    ```text
    -h -- print the file size in a human-readable format
    -s -- sort the files by size
    -l N -- limit the output to N files
    ```

### Logistics

1. You will provide a `Makefile` which builds one executable for `rarray` and a separate executable for `project03`
1. Remember not to commit executables or `.o` files to your repo

## Given

1. Lecture discussions will include multi-target `Makefiles`, reallocating memory, and getting information about files in the filesystem

## Rubric

1. 100 pts as shown by the autograder. No interactive grading for this project