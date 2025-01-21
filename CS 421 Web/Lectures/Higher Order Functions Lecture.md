---
tags:
  - lecture
---
Date:: [[January 30th, 2025]]
## Synopsis

A higher order function allows you to pass a function as an
argument to another function.  Sure, you could do this with
function pointers in C, but HOFs also allow you to have functions
create new functions and return them, store them in variables, and
call them at will.

Before watching the videos, consider the three functions below.
The first two have a lot of code duplication.  Most languages give
you no mechanism to avoid this.  Then consider the third function.
How could you call this function to provide the functionality of the
first two functions?

```haskell
incList [] = []
incList (x:xs) = x + 1 : incList xs

decList [] = []
decList (x:xs) = x - 1 : decList xs

map f [] = []
map f (x:xs) = f x : map f xs
```

## Videos
 - Introduction
 - Map and Foldr
 
## Handouts
 - [[/assets/handouts/hofs-pogil.pdf|Higher Order Functions Activity (pdf}]]
