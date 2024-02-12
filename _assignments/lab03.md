---
layout: assignment
due: 2024-02-20 23:59:59 -0800
permalink: assignments/lab03.html
title: Lab03 - Files, struct
github_url: https://classroom.github.com/a/mmfjAhJy
published: true
---

## Background

In C, it's very important to be careful when allocating memory, copying data between buffers, and working with files. In this lab, we will explore how to manage data in files, and also how to use `struct` to group relevant data. 

In project01, the C program tried to find a plaintext password for the given hash. However, hashing 30,000 different passwords for every input is highly redundant and inefficient. Most password crackers hash the passwords once and store the pair (hash, password) in a Dictionary file and use it for future cracking, thus called [Dictionary Attack](https://en.wikipedia.org/wiki/Dictionary_attack). 

In lab03, you will develop a C program: lab03.c that creates a dictionary file from 10,000 given passwords, their leet versions, and the trailing-1 versions, and uses this dictionary file to find a password that matches a given hash.  

## Requirements

1. You will develop a C program named `lab03` which 
    1. check if `dictionary` file exists. if not, 
        1. create a `struct` that stores (password, hash) pair.
        1. for each password among 10,000 given passwords, create three pairs of information (password, its hash), (the leet version of the password, its hash), and (the trailing-1 version of the password, its hash).
        1. writes all pairs out to a file named "dictionary".
    1. for the hash given as a command-line argument, find the corresponding password in the dictionary.
1. Each entry in dictionary will have a password (at most 64 chars and a NULL) and hash (at most 64 chars and a NULL), and you will keep those in one or more C `struct`. These entries will be written as a `struct` and read as a `struct`.
1. You will use the C file management functions to open, write, and close a file
1. You will handle error conditions **exactly** as shown in the example output
1. You will provide a `Makefile` and test your project with the `grade` script

## Given

1. C file management functions demo in lecture
1. Any code from project01

## Example Output
```sh
$ ./lab03 
dictionary built

$ ./lab03
dictionary exists

$ ./lab03 5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8
password

$ ./lab03 15e2b0d3c33891ebb0f1ef609ec419420c20e320ce94c65fbc8c3312448eb225
123456789

$ ./lab03 84f081273670181b0d00600d4972de62686806e8e98e14fd423dd3ad6f9e0f5b
niners

$ ./lab03 7e016a27dae18f63bb89e1455273332e4eab64a5308575ab9494dc78f06960bc
n!n3r$

$ ./lab03 ef60a458e0016857ade43406a7cfd256a904f8becd75c660b19ac72831f502d6
niners1

$ ./lab03 c9e100f0214a368bc599534b9d25877699aba73adb3b8691f2021de9eddf96c9
not found
```

## Rubric
1. Your lab will receive the score shown by the autograder
1. Deductions may be made if your code does not meet the above requirements
