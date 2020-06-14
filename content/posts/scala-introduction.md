---
title: "Scala Introduction"
date: 2020-06-13T11:45:32Z
draft: true
type: 'post'
tags: ['scala', 'programming-language']
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
    - Anonymous functions - `(x: Int) => x + 1`
    - Names functions - `val add1 = (x: Int) = x + 1`
- `Methods` are similar to `functions` with slight variation in syntax
    - `def add1(x: Int): Int = x + 1`
- `Classes` are defined by using `class` keyword.

      class Abc(name: String) {
            def say(): Unit = println(name)
      }
      val abc = new Abc("Ankush")
      abc.say() // Ankush
    - Instances of classes get compared with reference
    - Can inherit only one other class.
- `Case Class` is special case of class , instances of which are compared with value.

      case class Point(x: Int, y: Int)
    - No `new` is required to instantiate case class.
- `Object` are single instances of their own defination. For example- 

      object ResourceFactory {
          def create() : Int = {
             return 1 // random new resource id
          }
      }

      val newResourceId = ResourceFactory.create()
-  `Traits` are abstract data types containing fields and methods.
    - `Class` can extend multiple traits, but only one other class.
    
- `Main` method is required by JVM, which acts are entry point of Scala program.
   - Accepts a list of multiple strings.

### Data structures
- Int
- Boolean
- Double
- String

### Good practice for functions 
- When functions have no parameters, but have side-effects, you should declare it and call it with empty brackets ()



Source - https://docs.scala-lang.org/tour/basics.html