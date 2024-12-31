# krupka
## a CommonLisp interpreter

## Usage:

### Commands:

``repl``    Launch interactive interpreter

``run``     Interpret a .lsp source file

``compile`` Compile a .lsp source file into a binary


### Options:
``repl``
```
./source.lsp
--no-std
--include /path/to/file/or/dir
```
``run``
```
./source.lsp
--no-std
--include /path/to/file/or/dir
```
``compile``
```
./source.lsp
--no-std
--include /path/to/file/or/dir
-o /path/to/bin

```
# Built-in:
## Primitives
``Arithmetic``
```
+ - / *
```
``Comparisons``
```
=
> < <= >=
```
``Logical Operations``
```
not
```

``Functions``
```
apply
funcall
```
## Special:
``Control flow``
```
if
cond
```
``Function Creation and Quoting``
```
lambda
quote '
function #'
```
``Variable and Function Definitions``
```
let
let*
labels
defun
```
``Logical operators``
```
and
or
```
# STD - standard library of functions:
not to be confused with built-in functions and special-functions!

```
misc functions, eg. mapcar, first...
```

# Example krupka usage

## Running a file
### Command
``kurpka run ./example.lsp --include ./std -q``

``./example.lsp``
```lisp
; Definition of user functions

(defun add (a b)
  "Adds a and b"
  (+ a b))
(defun sub (a b)
  "Subtracts a and b"
  (- a b))

; Testing
(add 1 2 3) ; 5
(sub 5 2)   ; 3
```
### Output
```
5
3
```

## Using REPL
### Command
``kurpka repl``

### Output
```
krupka 0.1
(main, Dec 31 2024, 00:00:00)
[rustc 1.83.0 (90b35a623 2024-11-26)]
Type "(help)" for help

 (+ 1 2 3)
5
 (defun add (a b)
..  "Adds a and b"
..  (+ a b))
 (add 1 2)
3
 (invalid)
Error: krupka::parser::undefined_function

  × Call of an undefinded function
   ╭─[entry #1:1:1]
 1 │ (invalid)
   · ─────┬────
   ·      ╰── Function `invalid` not found
   ╰────
  help: `invalid` is neither a built-in function or
        an user defined function

 (add 1)
Error: krupka::parser::wrong_argument_count

  × Call of a function with incorrect count of arguments
   ╭─[entry #2:1:1]
 1 │ (add 1)
   ·      ┬
   ·      ╰── Function `add` takes 2 arguments
   ╰────

 (exit); or ^C to exit
```

## Compilation of a binary
### Command
``krupka compile ./example.lsp -o ./bin``

``./example.lsp``
```lisp
; Definition of user functions

(defun add (a b)
  "Adds a and b"
  (+ a b))
(defun sub (a b)
  "Subtracts a and b"
  (- a b))

; Testing
(add 1 2 3) ; 5
(sub 5 2)   ; 3
```
### Output
```
```

### Bash
```bash
 ./bin
5
3
```

# Misc

## Function information on return
### Command
``krupka repl``

### Output
```
 #'+
Function {name:Some("+"), origin:"Built-in"}

 #'Add
Function {name:Some("Add"), origin:"User"}

 (lambda (x) (* x x))
Function {name: None, origin:"User"}
```

## To be continued...