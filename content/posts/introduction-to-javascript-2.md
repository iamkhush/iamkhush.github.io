---
title: "Introduction to Javascript 2"
date: 2020-07-23T21:46:21Z
type: 'post'
tags: ['javascript', 'programming-language', 'Scope', 'variables']
series: 'Learning Javascript'
---

## Understanding Scope

The scope of a variable controls where it can be accessed from in the program.
It can be of 
- Global Scope
- Curly Bracket Scope
    - Function scope
    - Block scope ( if / for etc )


### Variable defination
Variables can be defined with `var`, `const` and `let` keywords.
- `var` keyword is globally scoped or function scoped where ever it is defined in.
- `let` and `const` keyword are block scoped.


### `this` keyword
- Different from how other languages use this.
- In JS land, value of this depends on how a function is called.
- `call` and `apply` helps in setting correct `this` value
   - the difference is in the way the arguments are provided
   - `apply` takes a array of arguments whereas `call` takes in individual arguments.


Source - https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/
    and  https://www.educative.io/courses/complete-guide-to-modern-javascript/m2vkA419vVG