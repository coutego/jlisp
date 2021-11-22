# jLisp
A Lisp intepreter implemented in Typescript

- [jLisp](#jlisp)
    - [Why?](#why)
    - [Getting started](#getting-started)
    - [Implementation](#implementation)
    - [What next](#what-next)
        - [Big things](#big-things)
            - [Object System](#object-system)
            - [Debugger](#debugger)
            - ["Compiler"](#compiler)
        - [Small things](#small-things)

## Why?
This is a project I did just for fun, so don't expect any advanced features or worry about performance, etc.
It only exists as a tool to teach myself how languages work. 

Also, I didn't know any Lisp, when writing this, so many things don't actually make sense.

## Getting started
(This has not been updated for more than a year. Good luck making it work).

Make sure you have npm installed on your machine and you cloned this repository. Then write

```bash
npm run full
```

That will install dependencies, compile the source code, run the tests and, last, run the
REPL.

Of course, you don't want to wait for the installation and compilation each time you change
something, so 'tsc -w' is your friend and then you can use the normal npm commands:

```bash
npm install   # Normally only needed the first time
npm run test  # This runs the tests and is what you execute all the time
npm start     # It runs the REPL
```

You can try whatever short pieces of code in the REPL. By now it should be robust enough to
not die when errors occur. In order to try less trivial pieces of code, you can use the
'jlisp.js' program that you can find in the 'dist' folder in order to load and execute files. You can invoke the program like this:

```bash
node jlisp.js my_program.lisp
```

where 'my_program.lisp' is the program you want to try.

If you want to modify some things inside the interpreter itself, at the end of this README.md file there are some smallish tasks
that would be useful to do.

## Implementation
The tokenizer and parser are contained in the files ./tokenizer.ts and ./parser.ts. Being Lisp the syntaxless language
that it is, those two components are quite trivial. The parser has support for quoting, which makes it slightly
less trivial than it should otherwise.

The interpreter is located in the file ./interpreter. It is very minimalistic. 
It only knows how to load and run macros and intepret existing code. There are no
hardcoded macros of functions inside it, only calls to the macros and functions defined in the ./functions.ts
and ./macros.ts. As such, the interpreter and macro expander is also quite trivial.

The small number of functions already implemented are contained in the file ./functions.ts. There are some
functions implemented as native (Typescript) code and a few more implemented in Lisp itself.

Most of the less simple code is located in ./macros.ts. There there are the fundamental macros 
'if', 'lambda' (also called 'fn'), 'define', 'defn', 'eval', ... The interpreter simply loads those macros in the
runtime at the start, but they are not otherwise special. They can even be replaced by user code by simply defining new
macros with the same names.

Note that all the values are strongly typed at runtime. You can check the types of the language in the file ./parser.ts

## What next
### Big things
#### Fix the special form implementation
I implemented the special forms in a complete wrong way, as a sort of functions. Special forms should have special treatment. This should be reimplemented.

