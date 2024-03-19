---
layout: assignment
due: 2024-03-19 23:59:59 -0800
permalink: assignments/project03.html
title: Project03 - Elastic Array, File Stat
github_url: https://classroom.github.com/a/K1C_qhBi
published: true
---

## Requirements

### Part 1

1. In C, arrays have fixed size, and are not dynamically resizable as in Python and Java
1. You will implement a resizable array in C, called `rarray`. The header file for rarray is given in the inclass repo
1. Test cases are numbered 1 to 5, with the test case name being the first 
argument, followed by an array of integers
1. Example output
    ```
    ./rarray 2 100 200 300
    100
    200
    300
    ```
1. The code for each test case is given in `rarray_main.c` in the inclass repo. The function of each test case is
    1. Create a resizable array of zero length
    2. Create a resizable array and add the given array into the array as 4-byte elements. Print the array values by providing a callback function pointer to `rarray_iterate()`
    3. Create a resizable array and get the value of the 0th element
    4. Create a resizable array and remove the 0th element, resizing to the new smaller size by using `memcpy()`
    5. Create a resizable array and sort its contents using `rarray_sort()` by providing a callback function pointer for `qsort()`

### Part 2

1. Now that you have a resizable array, you can use it to traverse the filesystem and make a list of files, even if you don't know how many there are.
    ```text
    $ ./project03 -l 10 /usr/include
    /usr/include/python3.9/pyconfig-64.h 47979
    /usr/include/openssl/md5.h 1696
    /usr/include/openssl/aes.h 3752
    /usr/include/openssl/mdc2.h 1441
    /usr/include/openssl/asn1.h 60914
    /usr/include/openssl/modes.h 10786
    /usr/include/openssl/asn1_mac.h 398
    /usr/include/openssl/obj_mac.h 228668
    /usr/include/openssl/asn1err.h 7731
    /usr/include/openssl/objects.h 6848    
    ```
1. Options
    ```text
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