#PyBasic

##Introduction

A simple BASIC interpreter written in Python. It is based heavily on material in the excellent book "Writing Interpreters and Compilers for the Raspberry Pi Using Python" by Anthony J. Dos Reis, although I have had to adapt the Python interpreter presented in the book to work with the BASIC programmin language. the interpreter therefore adopts the key techniques for interpreter and compiler writing, the use of a lexical analysis stage followed by a parser which implements the context free grammar representing the target programming language.

The interpreter is a homage to the home computers of the early 1980s, and when executed, presents an interactive prompt ('>') typically of such a home computer. Commands to run, list, save and load BASIC programs can be entered at the prompt as well as program statements themselves. 

The BASIC dialogue that has been implemented is slightly simplified, and naturally avoids machine specific instructions, such as those concerned with sound and graphics for example. It allows a limited range of arithmetic expressions composed of multiplication, division, addition and subtraction (including parenthesised subterms). Variable types follow the typical BASIC convention: they can either be strings or numbers (the latter may be integers or floating point).

The interpreter can be invoked as follows:

```
$ python interpreter.py
```

*This project is still a work in progress and under active development*

##Commands

Programs may be listed using the LIST command:

```
> LIST
10 LET I = 10
20 PRINT I
```

A program is executed using the RUN command:

```
> RUN
10
```

A program may be save to disk using the SAVE command:

TODO

Saving is achieved by pickling the Pythin object that represents the BASIC program, i.e. the saved file is *not* a textual copy of the program statements.

The program may be re-loaded (i.e. unpickled) from disk using the LOAD command: 

TODO

##Programming language constructs

###Statement structure

As per usual in old school BASIC, all program statements must be prefixed with a line number which indicates the order in which the statements may be executed. There is no renumber command to allow all line numbers to be modified. A statement may be modified or replaced by re-entering a statement with the same line number:

```
> 10 LET I = 10
> LIST
10 LET I = 10
> 10 LET I = 200
> LIST
10 LET I = 200
```

Note that all statements, including variable names are case insensitive (in fact, all lower case characters are converted to upper case internally by the lexical analyser).

###Comments

The REM statement is used to indicate a comment, and occupies an entire statement. It is no effect on execution:

```
> 10 REM THIS IS A COMMENT
```

###Assignment

Assignment may be made to number variables and string variables (string variables are distinguished by their dollar suffix). The interpreter will enforce this division between the two types:

```
> 10 LET I = 10
> 20 LET I$ = "HELLO"
```

Note that 'I' and 'I$' are considered to be separate variables. Note that string literals must always be enclosed within double quotes (not single quotes). Using no quotes will result in a syntax error.

The LET keyword is also optional:

```
> 10 I = 10
```

###Printing to standard output

The PRINT statement is used to print to the screen:

```
> 10 PRINT 2 * 4
> RUN
8
> 10 PRINT "HELLO"
> RUN
HELLO
```

###GOTO

Like it or loath it, the GOTO statement is an integral part of BASIC, and is used to transfer control to the statement with the specified line number:

```
> 10 PRINT "HELLO"
> 20 GOTO 10
> RUN
HELLO
HELLO
HELLO
...
```

###GOSUB

TBD

###Loops

TBD

###Conditional branching

TBD

###Open issues

Currently there is no way to terminate an infinite loop in a BASIC program without terminating the intepreter itself (e.g. using Ctrl-C).
