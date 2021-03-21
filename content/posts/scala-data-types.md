---
title: "Scala Data Types"
date: 2020-06-14T19:07:10Z
type: 'post'
tags: ['scala', 'programming-language', 'Data Types']
series: 'Learning Scala'
summary: 'Going through Scala Data types'

---

### Scala's unified type system

![](https://docs.scala-lang.org/resources/images/tour/unified-types-diagram.svg)

- `Any` is the super type
   - Defines methods like - `equals`, `hashCode`, `toString`
- `AnyVal` represents value types.
    - Double
    - Float
    - Long
    - Int
    - Short
    - Byte
    - Char
    - Unit - Only one instance can be there - `()`
    - Boolean
- `AnyRef` represent refernce types like `List`
- `Nothing` is subclass for all value types.
- `Null` is subclass for all reference types. **Should not be used in Scala code.**

### Type Casting
Type casting is unidirectional

![](https://docs.scala-lang.org/resources/images/tour/type-casting-diagram.svg)


Source - https://docs.scala-lang.org/tour/unified-types.html