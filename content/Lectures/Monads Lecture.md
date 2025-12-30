---
tags:
  - lecture
---
## Synopsis

Monads are a famous feature of the <Sc>Haskell</Sc> programming language, and
have started to find their way in many other languages as well. In this
period we’ll cover type classes, which provide the abstraction necessary
for monads (and many other things). Then we’ll cover the functor type
class, which allows us to define a `map`-like function for any type we
want. Finally, we’ll cover monads themselves.

One feature about monads is that they inspire programmers to write blog
posts and tutorials about them. For the most part, they tell you more
about the state of mind that that particular programmer had when monads
finally “clicked” than about monads themselves. The article below, *You
could have invented monads*, is a refreshing change, and I recommend you
read it, even before watching my video.

## Videos
 - [[Monads]]
 
## Further Reading
 - [The Typeclassopedia](https://wiki.haskell.org/Typeclassopedia) Yes, this was linked from the Typeclass lecture.
 - [You could have invented monads](http://blog.sigfpe.com/2006/08/you-could-have-invented-monads-and.html) This blog post walks through how monads may have been "discovered" by a normal programmer.
 - [Monads for Functional Programming](http://citeseer.ist.psu.edu/viewdoc/summary?doi=10.1.1.100.9674) This paper talks about writing an interpreter and adding abilities simply by changing which monad we give to it.
 - [Functors, Applicatives, and Monads in Pictures](http://adit.io/posts/2013-04-17-functors,_applicatives,_and_monads_in_pictures.html)
 - [A monad is a monoid in the category of endofunctors, what's the problem?](https://www.reddit.com/r/math/comments/ap25mr/a_monad_is_a_monoid_in_the_category_of/) That phrase is something you will hear from time to time about the link between Category Theory and Haskell monads.  This article explains the math behind it if you are interested.  
   As the [comments](https://www.unix.com/what-is-on-your-mind-/108501-line-2238-unix-v6-comment-you-not-expected-understand.html) in the Unix V6 source code say, "you are not expected to understand this".
