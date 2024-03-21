---
layout: assignment
due: 2024-03-26 23:59:59 -0800
permalink: assignments/lab04.html
title: Lab04 - Lexical Analysis
github_url: https://classroom.github.com/a/BV8E7K4Z
published: true
---

## Background

Over the next few weeks, we will build a scanner, parser, and interpreter for a little language which demonstrates basic arithmetic, number bases, and bitwise operations.

## Requirements

1. For this lab, you will build a scanner for the language described below. We will address parsing and interpretation in subsequent assignments.
1. You must provide a `Makefile` which builds an executable called `lab04`
1. You must build the token table yourself, without using C `strtok()`
1. Use the techniques we learned for reading files and analyzing text to build up a linked list of tokens
1. You may use any of the code I showed, or you can make up your own if you prefer
1. Print the token IDs and names out exactly as shown to get credit for correctness

## Example Output

```
$ ./lab04 "1 + 2"
TK_INTLIT("1")
TK_PLUS("+")
TK_INTLIT("2")
TK_EOT("")

$ ./lab04 "(100 / 0x32) * 0b10"
TK_LPAREN("(")
TK_INTLIT("100")
TK_DIV("/")
TK_HEXLIT("32")
TK_RPAREN(")")
TK_MULT("*")
TK_BINLIT("10")
TK_EOT("")
```

We will define the set of acceptable tokens using Extend Backus-Naur Form (EBNF)
Here is the EBNF for this lab:
```
tokenlist   = (token)*
token       = intlit | binlit | hexlit | symbol 
intlit      = digit (digit)*
binlit      = '0b' bindigit (bindigit)*
hexlit      = '0x' hexdigit (hexdigit)*
symbol      = '+' | '-' | '*' | '/' | '(' | ')'
digit       = '0' | ... | '9'
bindigit    = '1' | '0'
hexdigit    = digit | 'a' | ... | 'f' | 'A' | ... | 'F'
whitespace  = ' ' | '\t'  # Ignore
```

Here are some definitions you should use in your implementation:
```c
#define SCAN_TOKEN_LEN 32

enum scan_token_enum {
    TK_INTLIT, /* -123, 415 */
    TK_BINLIT, /* 0b10, 0b1001 */
    TK_HEXLIT, /* 0x7f, 0x12ce */
    TK_LPAREN, /* ( */
    TK_RPAREN, /* ) */
    TK_PLUS,   /* + */
    TK_MINUS,  /* - */
    TK_MULT,   /* * */
    TK_DIV,    /* / */
    TK_EOT,    /* end of text */
};

#define SCAN_STRINGS {\
    "TK_INTLIT",\
    "TK_BINLIT",\
    "TK_HEXLIT",\
    "TK_LPAREN",\
    "TK_RPAREN",\
    "TK_PLUS",\
    "TK_MINUS",\
    "TK_MULT",\
    "TK_DIV",\
    "TK_EOT"\
};

struct scan_token_st {
    enum scan_token_enum id;
    char name[SCAN_TOKEN_LEN + 1];
    struct scan_token_st *next;
};

struct scan_table_st {
    struct scan_token_st *head;
    int len;
};
```

## Implementation Notes

1. The way to think about implementing a scanner given the EBNF is to create a function that will scan one token in the input string each time it is called. You need to figure out the starting character for each of the elements on the right-hand side of the token rule in the EBNF:
    ```
    token       = intlit | binlit | hexlit | symbol
    ```
1. For the one-character elements such as symbol, simply compare the next character in the input text to each of the possible one-character elements. If you find a match, then you create a corresponding token.
1. For multi-character elements such as intlit, binlit, and hexlit you will first see if the current character matches the beginning of one of these rules:
1. For an intlit, the first character must be a digit.
1. For a binlit, the first character must be a '0', and the second character must be a 'b'
1. For a hexlit, the first character must be a '0', and the second character must be an 'x'
1. Once you have determined that you are scanning one of the literal types, you should scan acceptable characters for that literal type until you get to a character which is not acceptable for that literal type.
1. Your scanner should ignore whitespace
1. You implementation should have the following functions:
    ```c
    void scan_table_init(struct scan_table_st *tt);
    void scan_table_scan(struct scan_table_st *tt, char *input);
    void scan_table_print(struct scan_table_st *tt);
    ```
