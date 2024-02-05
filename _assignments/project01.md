---
layout: assignment
due: 2024-02-13 23:59:59 -0800
permalink: assignments/project01.html
title: Project01 - Password Analyzer
github_url: https://classroom.github.com/a/rmIRHEP8
published: true
---

## Background

Passwords are a fundamental part of computer security, and yet commonly reused. Once passwords are compromised from one website, hackers use the same password on other websites, aka [Credential Stuffing](https://owasp.org/www-community/attacks/Credential_stuffing). 

In this assignment, we will implement [Dictionary Attack](https://en.wikipedia.org/wiki/Dictionary_attack). Hackers use Dictionay Attack to learn the actual passwords from stolen password files.

## Requirements

1. You will develop a C program which takes a hashed password (64 characters in length) on the command line.
1. Your program will compare the given hash with:
    1. The hash of each of a list of 10,000 common passwords (10k tests)
    1. The hash of each of the 10,000 passwords after substituting common "l33t speak" transformations like 'e' to '3' (10k-l33t tests)
    1. The hash of each of the 10,000 passwords with a '1' added to the end (10k-plus1 tests)
1. If the given hash matches any of those hashes, your program should print the clear-text password of the match. Otherwise, print "not found".
1. Your program must be called `project01` and must be built by a `Makefile` you provide.
1. No credit will be given for projects which hard-code the hashes from the test cases and print the expected result without computing the result as described above.

## Given

1. When you accept the assignment using the link above, your repo will contain the following given code:
    1. `passwords.h` and `passwords.c` which respectively declare and define the list of 10,000 common passwords
    1. `sha256.h` and `sha256.c` which respectively declare and define the code to compute a SHA-256 hash digest
    1. `project01.c` which shows how to use the SHA-256 functions.
1. Although there are a large number of l33t substitutions, we will use these common ones:
    1. Change 'o' to '0'
    1. Change 'e' to '3'
    1. Change 'i' to '!'
    1. Change 'a' to '@'
    1. Change 'h' to '#'
    1. Change 's' to '$'
    1. Change 't' to '+'
1. The test case for plus1 is separate from the test case for l33t, so yankees1 should match yankees, but y@nk33s1 should not match yankees. 
1. If you want to test some password hashes, there are many SHA-256 calculators online, including [this one](https://xorbin.com/tools/sha256-hash-calculator)

## Example Output

```sh
$ ./project01 5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8
password

$ ./project01 15e2b0d3c33891ebb0f1ef609ec419420c20e320ce94c65fbc8c3312448eb225
123456789

$ ./project01 84f081273670181b0d00600d4972de62686806e8e98e14fd423dd3ad6f9e0f5b
niners

$ ./project01 7e016a27dae18f63bb89e1455273332e4eab64a5308575ab9494dc78f06960bc
n!n3r$

$ ./project01 ef60a458e0016857ade43406a7cfd256a904f8becd75c660b19ac72831f502d6
niners1

$ ./project01 c9e100f0214a368bc599534b9d25877699aba73adb3b8691f2021de9eddf96c9
not found
```

## Rubric

1. Your project will be graded using autograder for correctness. You will need to `git pull` in the tests repo.
    1. 50 pts: passes 10k tests
    1. 20 pts: passes 10k-l33t tests
    1. 20 pts: passes 10k-plus1 tests
2. And manually for style
    1. 10 pts: [readable coding style](https://github.com/usfca-cs-tools/docs/blob/main/c-style.md), no build products in repo
