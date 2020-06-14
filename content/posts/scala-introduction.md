---
title: "Scala Introduction"
date: 2020-06-13T11:45:32Z
draft: true
type: 'post'
---

### Significant points of Scala

- Developed by Martin Odersky in 2004. 
- Is MultiParadigm - a blend of Functional and Object Oriented Paradigms
- Is statically typed
- Heavily uses Java libraries
- Encourages use of immutable data structures

### Basics
- `Expressions` are computable statements. For example  `1+1`
- `Values` are names for results for expressions. Example `val x = 1 + 1`
   - These are immutable
- `Variables` are mutable names for expression results. Example `var x = 1 + 1`
- `Blocks` are expressions combined together within a `{}`
    - Resukt of last expression in block is the result of the block as well.
- `Functions` are expressions that have params
    - Anonymous functions - `(x) => x + 1`
    - Names functions - `val add1 = (x) = x + 1`
    


### Data structures
- Int
- Boolean
- Double
- String

### Good practice for functions 
- When functions have no parameters, but have side-effects, you should declare it and call it with empty brackets ()



Source - https://docs.scala-lang.org/tour/basics.html