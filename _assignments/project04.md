---
layout: assignment
due: 2024-04-09 23:59:59 -0800
permalink: assignments/project04.html
title: Project04 - Expression Interpreter
github_url: https://classroom.github.com/a/3iNNokUO
published: false
---

## Requirements

1. In this project, you will evolve the scanner and parser you developed in recent labs.
1. You will add support for new language elements as shown in the EBNF below. Bitwise operators in C are explained [here](https://www.tutorialspoint.com/cprogramming/c_bitwise_operators.htm).
1. You will add an evaluation (interpretation) stage to our little language. Your interpreter will walk the parse tree (AST) depth-first, evaluating the expressions defined by the nodes. 
1. You will print the expression's value in base 2, base 10, or base 16, using the `-b` flag in command line input.
1. `-e` and `-b` flags may be given in any order. (See examples below)
1. All numbers are assumed to be 32 bits wide, so your output for base 2 and base 16 numbers should include leading zeros.

## EBNF Enhancements
1. The EBNF grammar for the scanner adds support for binary (`oper2`) bitwise operators in the `symbols` production 
    ```
    tokenlist  = (token)*
    token      = intlit | hexlit | binlit | symbol
    symbol     = '+' | '-' | '*' | '/' | '>>' | '<<' | '~' | '&' | '|' | '^'
    intlit     = digit (digit)*
    hexlit     = '0x' | hexdigit (hexdigit)*
    binlit     = '0b' ['0', '1'] (['0', '1'])*
    hexdigit   = 'a' | ... | 'f' | 'A' | ... | 'F' | digit
    digit      = '0' | ... | '9'
    # Ignore
    whitespace = ' ' | '\t' (' ' | '\t')*
    ```
1. The EBNF grammar for the parser adds support for unary (`oper1`) bitwise not operator (`~`)
    ```
    program    = expression EOT
    expression = operand (operator operand)*
    operand    = intlit
               | hexlit
               | binlit
               | '-' operand
               | '~' operand
               | '(' expression ')'
    ```

## Example Output
```
$ ./project04 -e "10 + 1"
11
$ ./project04 -e "10 + 1" -b 16
0x0000000B
$ ./project04 -e "0x0A" -b 10
10
$ ./project04 -e "0b1010 | 0b0101" -b 16
0x0000000F
$ ./project04 -b 10 -e "(2 * (0b1111 & 0b1010))"
20
$ ./project04 -b 2 -e "(0xF << 0x4) + 1"
0b00000000000000000000000011110001
```

## Debugging Tips
1. Evaluation should do a depth-first recursion until the base case (`intval`) is encountered. Expressions of type `oper1` and `oper2` should recurse over their child node(s).
1. If you have bugs, narrow down the problem
    1. Is it a scanning bug? Print your scan table to make sure it's correct
    1. Is it a parsing bug? Print your parse tree to make sure it's correct
    1. Is it an evaluation bug? Print the result at each level of recursion to make sure it's correct
    1. Is it an output conversion bug? Print the parser's return value as an `int` separately from its conversion into a string.
1. Use gdb to help you
    1. Set breakpoints at the stage of interpretation where the bug can be seen.
    1. Use next, step, and print to look at the values of your variables and compare to what you expect.

## Rubric
1. 80 pts: automated tests
1. 20 pts: neatness 
1. 2 pts: extra credit. Add support for outputting binary and hexadeximal numbers which are 8-bits wide, or 16-bits wide, in addition to 32 bits. Use the command-line parameter `-w` to specify the width, e.g.
    ```
    $ ./project04 -e "0xA + 1" -b 2 -w 8
    0b00001011
    $ ./project04 -e "(0xA + 2) - 1" -b 2 -w 16
    0b0000000000001011
    ```
