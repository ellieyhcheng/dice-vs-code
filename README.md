# Dice Syntax Highlighter

Provides syntax highlighting for the probabilistic programming language [Dice](https://github.com/SHoltzen/dice).

## Installation
This extension is not on VS Code Marketplace as of right now. You can install it manually by downloading the release and running:
```shell
$ code --install-extension dice-vs-code-1.0.1.vsix
```

## Features

Syntax Highlighting for Dice, based on the current syntax:
```
ident := ['a'-'z' 'A'-'Z' '_'] ['a'-'z' 'A'-'Z' '0'-'9' '_']*
binop := +, -, *, /, <, <=, >, >=, ==, !=, &&, ||, <=>, ^

expr := 
   (expr)
   | true
   | false
   | int (size, value)
   | discrete(list_of_probabilities) 
   | expr <binop> expr
   | (expr, expr)
   | fst expr
   | snd expr
   | ! expr
   | flip probability
   | observe expr
   | if expr then expr else expr
   | let ident = expr in expr

type := bool | (type, type) | int(size)
arg := ident: type
function := fun name(arg1, ...) { expr }

program := expr 
        | function program
```
as well as for comments. 

## Technical Details

### Comments
Lines beginning with // are mapped to comment.line

### Constants
- true and false are mapped to constant.language
- numbers (integers and floats) are mapped to constant.numeric

### Operators
- Binops are mapped to keyword.operator.binop
- !, fst, and snd are mapped to keyword.operator.unop

### Variables
Idents are mapped to variable.name

### Control
- if-then-else and let-in are mapped to keyword.control.[if/then/else/let/in]

### Functions
- keyword fun is mapped to keyword.other.function
- function name is mapped to entity.name.function
- parameters are mapped to variable.name
- types are mapped to entity.name.type

### Probability Related Keywords
- observe is mapped to keyword.other.probability.observe
- int(size,value) is mapped to keyword.other.probability.int
- discrete(probabilities) is mapped to keyword.other.probability.discrete
- flip probability is mapped to keyword.other.probability.flip

### Punctuation
- Punctuations (that aren't operators) are mapped to punctuation.[punctuation-name\].[open/close]
- Includes: ()[]{},
