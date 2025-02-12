---
tags:
  - lecture
---
Date:: [[March 25th, 2025]]
## Synopsis

We have seen a few different kinds of parsers to this point.  They all work by constructing
state machines to handle the parsing.  A new class of parsers has started to become popular
lately.  Combinator parsers use functions to represent parsers, and they can be composed together
to make more sophisticated parsers.

We will show how to build one of these from the ground up, and make use of monads to give us
a natural syntax.


## Videos
 - [[Combinator Parsing]]
## Handouts
 - [[combinator-parsing-pogil.pdf|Combinator Parsing Activity (PDF)]]
## Further Reading
 - [Monadic Parser Combinators (Graham Hutton)](http://www.cs.nott.ac.uk/~pszgmh/monparsing.pdf) This paper is a tutorial about monads and parser combinators. It is written in a language called Gopher, a precursor to Haskell.
