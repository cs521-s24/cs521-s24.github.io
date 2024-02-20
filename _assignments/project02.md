---
layout: assignment
due: 2024-02-27 23:59:59 -0800
permalink: assignments/project02.html
title: Project02 - File Find utility
github_url: https://classroom.github.com/a/SD1_I44o
published: true
---

## Requirements

1. You will write a C program and `Makefile` which find files in a given directory
    ```text
    $ ./search foo.txt
    ./bar/baz/foo.txt
    ```
1. Your solution must be recursive; that is, a function which calls itself
1. Your solution will search using the following Boolean command-line flags
    ```text
    -d include directories only (no files)
    -e include exact matches only (no partial matches)
    -f include files only (don't print directories, but recurse anyway)
    -h include hidden files (leading '.')
    -H display help message
    ```
and the following arguments
    ```text
    -c text (match only if text appears in file)
    -l depth-limit
    ```

## Given

1. We have previously discussed structured types, working with pointers,
memory-safe string operations, and error handling. You should utilize those 
tools in this project
1. In lecture, we will demonstrate C versions of 
    1. Recursive functions
    1. Parsing command line arguments
    1. Using disk and file APIs
    1. Using bit fields
1. Use `git pull` in the `tests` repo to get the test cases for this assignment

## Design Decisions

In order to make the project auto-gradable, a few design decisions have been made
1. Directories can not have contents (`-c` and `-d` are incompatible)
1. Recursion into child directories happens before entries in the current directory are printed

## Rubric

1. 80 pts - correctness as shown by the autograder
1. 20 pts - interactive grading
    1. You must attend a 1:1 interactive grading meeting with the instructor or TA to get
    credit for the project. No partial credit is available for code without a meeting.
    1. We will meet during the first lecture time slot after the due date
    1. Be prepared to show your solution in a terminal editor (`micro`, `vim`, etc.) in a `clab` container. VS Code, Sublime, web browsers, etc. are not acceptable
    1. Be prepared to explain how your solution works, including correct use of the given material.
    1. Interactive grading includes [coding style](https://github.com/usfca-cs-tools/docs/blob/main/c-style.md)