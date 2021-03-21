---
title: "Introduction to Javascript 2"
date: 2020-07-23T21:46:21Z
type: 'post'
tags: ['javascript', 'programming-language', 'Scope', 'variables']
series: 'Learning Javascript'
summary: 'Some notes about Javacript part 2, covering scope, hoisting etc'
---

## Understanding Scope

The scope of a variable controls where it can be accessed from in the program.
It can be of 
- Global Scope
- Function scope
- Block scope ( if / for etc )


### Variable defination
Variables can be defined with `var`, `const` and `let` keywords.
- `var` keyword is function scoped
- `let` and `const` keyword are block scoped.


### `this` keyword
- Different from how other languages use this.
- In JS land, value of this depends on how a function is called.
- `call` and `apply` helps in setting correct `this` value
   - the difference is in the way the arguments are provided
   - `apply` takes a array of arguments whereas `call` takes in individual arguments.

### Hoisting
 - All variable declarations are hoisted on the top of their scope.
 - Hence they are processed before the code gets executed.
 - `var` is set as undefined and can be accessed before declaration.
 - `let` and `const` cannot be accessed and throws a referenceError if tried.

Sources
- https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/
- https://www.educative.io/courses/complete-guide-to-modern-javascript/m2vkA419vVG
- https://www.educative.io/courses/complete-guide-to-modern-javascript/g76wvk6D9M9