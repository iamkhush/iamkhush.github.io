---
title: "Es6 Javascript"
date: 2020-07-25T22:14:11Z
draft: true
type: 'post'
---

## Iterables and Looping

- For looping over iterables, ES6 provides us with `for of` loop
- For looping over an object, 
    - Use `Object.keys` or `.values` in `for of` loop.
    - Also, can use a `for in` loop where it iterates of `enumarable` properties.
        - It will however iterate on keys not value of objects.

 
## Symbols
- New primitive added in ES6
- Always unique
- Useful for keys with same names but different values
- Not enumarable

## Classes
- Just a wrapper around prototype inheritence.
- Can have `static` method, `setters` and `getters`.

## Generators
- Similar to Python's syntax for generators.
- Use the `yield` keyword to temporarily hald the program and return the `yield`ed values
- Use the `next` method to continue execution where it was left of


