---
tags:
  - lecture
---

## Synopsis

If a language is to be extensible at all, it has to give the programmer a way to define new types.
<Sc>Haskell</Sc> provides user-defined disjoint types as one of its solutions to this problem.  A disjoint
type is a type that has more than one kind of constructor.  These turn out to be very useful in
representing expressions of a programming language internally, so we will make heavy use of them.

We will also cover [[Pairs]], which we will use a lot, and [[Records]], which we will use infrequently.
## Videos
 - [[Product Types]]
 -  [[Sum Types, Part 1]]
 - [[Sum Types, Part 2]]
## Activitites
 - [[/assets/handouts/adt-pogil.pdf|Algebraic Data Type Activity (pdf)]]
## Further Reading
 - [Generalized Algebraic Data Types](https://en.wikibooks.org/wiki/Haskell/GADT)
   There is a more general version of the product types supported by the language.  They are more powerful than the types we will use in class, and you may find them useful in your own programming.
