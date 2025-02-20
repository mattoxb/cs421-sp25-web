---
id: Continuation Passing Style
aliases: []
tags: []
---


<iframe id="kmsembed-1_zmjszn1u" width="640" height="394" src="https://mediaspace.illinois.edu/embed/secure/iframe/entryId/1_zmjszn1u/uiConfId/55779922/pbc/113245372/st/0" class="kmsembed" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" referrerPolicy="no-referrer-when-downgrade" sandbox="allow-downloads allow-forms allow-same-origin allow-scripts allow-top-navigation allow-pointer-lock allow-popups allow-modals allow-orientation-lock allow-popups-to-escape-sandbox allow-presentation allow-top-navigation-by-user-activation" frameborder="0" title="Continuation Passing Style"></iframe>

## Slides
- [[05.1.1-cps.pdf|Continuations (PDF)]]

# Continuations Transcript

## Slide 1 - Title

Hello everyone, and welcome to CS 421.

Today we are going to talk about Continuation Passing Style. Continuations are a
functional representation of "what comes next" in a computer program or
computation.   We can pass these continuations into functions just like any other
higher order function, and we can use them to do some really cool things!

## Slide 2 - Objectives

Here are our objectives for today.  After you have worked through the content of
this video, you will be able to explain what Continuation Passing Style is,
give an example of a programming technique that CPS enables, and write a recursive
function using CPS.  This will be a warm-up for the followup video, which will
show you how to take an existing function and transform it into CPS.

## Slide 3 - Direct Style

Here is some example code to consider.  I have written three simple functions,
`inc`, `double`, and `half`, that do the obvious things.  Next I compose them
together as `inc (double (half 10))` and save the output in the variable result.

Think about what is happening when we run this.  Half will receive the value 10,
process it, and then return it back.  The function `double` will continue the
computation by consuming `half`'s output, processing it, and returning it back.  Finally
`inc` will continue the computation by consuming `double`'s output, processing it,
and returning it back to be stored in the variable `result`.

## Slide 4 - The Continuation

I'm sure you noticed that I talked about functions "continuing" the computation.

We can make this idea very explicit.  Imagine that we take an expression and
"punch out" a subexpression.  In this case, let's punch `half 10` out of its
containing expression.  That leaves an expression with a hole in it, which we can
represent using these strange looking brackets.  (As an aside, these brackets
are called *semantic brackets*.  We make them by doubling up square brackets, and
use them frequently when talking about transformations that work on code.)

We can call this expression-with-a-hole a *context*.  After `half 10` runs, it's
result will be placed into this context.  If we turn this context into a function
we can call it a *continuation*.

## Slide 5 - Making Continuations Explicit

Let's see how to do that now.  Since a hole is just a spot where we can put a value
later, we can represent that easily by wrapping it in a lambda, and letting the
parameter of the lambda represent the hole.  In this case, let the continuation be
"lambda v -> inc (double v)".  For some reason it is common to name the continuation's
argument v.  If the word *result* began with the letter v that would have worked for me,
but oh well...

Now the next thing we are going to do is augment `half`. It will take a second
parameter, which we call its continuation. By convention the continuation
argument is usually given a name beginning with the letter k.  At least the
work *continuation* starts with the k sound.

When `half` is done, it's going to pass its result to the continuation argument.
This has a very interesting effect.  When we use continuation passing style, we can
imagine that the function `half` never returns.  Remember in the higher order function
lecture when we talked about using `map` to reduce the amount of code we needed to write?
We could simply pass an operation into `map` and it would recurse over the list for us.
A similar thing is happening here, but this time what we are parameterizing is
**how a function returns its value to the rest of the program**.

Haskell doesn't have this, but many languages have an explicit `return` keyword
that functions use to exit.  You can imagine what we are doing here is parameterizing
the return keyword.

## Slide 6 - Properties of CPS

To summarize...

We have seen two kinds of recursion so far.  There is *direct style*, which is what
most people would think of as "normal" recursion.  There's also tail recursion, or
accumulator recursion, when our recursive calls happen in a function's tail position.

Now we are going to go a step further; we are going to assume that when a function
passes its result to a continuation, that the call to the continuation never returns.
Because the call happens in tail position, it is likely that the bit about not returning
is actually true; the compiler is going to optimize the underlying machine code to
remove the intermediate stack frames.

## Slide 7 - Comparisons

Let's look at some examples.  In this slide I've converted the rest of the functions
from our initial example to use CPS.  `inc` and `double` are modified similarly to
`half`.  The interesting thing is `result`.  The continuation fed into `half 10`
stores the output in `v1` and passes `v1` into `double`.  But now `double` wants a
contination, so we give it one that stores `double`'s output into `v2`.  Finally,
we can pass `v2` into `inc`.  `inc` wants a continuation, but we are done, so we
pass in `id` to make it return the result back to the main program.  So notice:
we often will have occasion to nest one continuation inside of another one.

## Slide 8 - CPS and Imperative Style

One interesting thing people have noticed about CPS is how similar it is to
imperative style.  If you rewrite the functions as := style assignments you
get something that looks like an imperative program.

## Slide 9 - The GCD Program

Let's look at an instance where CPS actually gets us something.  This function
here computes the greatest common divisor of $a$ and $b$.  It's not particularly
slow, but it does have to do a bit of modular arithmetic.

Now imagine that we wanted to take the GCD of an entire list of numbers.  We
can call this function GCD-star, and it's source is on the next slide.

## Slide 10 - GCD of a List

This is just a simple folding recursion.  The function will traverse itself down
the list until it hits the empty list, and then compute the GCD of everything as
it returns.

Now imagine that there was a 1 near the beginning of the sequence.  What would
happen?  The GCD of 1 and anything is 1, so all the GCD operations that happened
on the rest of the list would be wasted.  The same kind of thing happens if we
wanted to take the product of all the elements of a list, and somehow there was
a zero in that list.  A lot of multiplications would have occured uselessly.

There are several things we could do, like checking the list first to see if
there was a 1 in it, but this is a lecture about continuations, so let see how
we can use continuations to fix this.

## Slide 11 - Continuation Solution

I'm going to talk about this function, but you might want to pause this video
and take a look at it first.

(pause)

There are a few things to notice.  The first is that we have an auxiliary function
`aux`, which uses its own continuation name `newk`.  We initialize `newk` by calling
`aux` with `k`.  This has an interesting effect: whenever `aux` is running it has
two separate continuations in its scope: it's own current continuation `newk`, and the
`gcdstar`-wide continuation `k`.  There is nothing stopping `aux` from calling either
one of these.

In the base case, `aux` calls `newk` with the base case value 0.
In the usual recursive case recursive case `aux` creates a new continuation by wrapping
a lambda around the current continuation.  The parameter `res` will get the result of
the recursive call to `aux`, and call `gcd` on that and `x`, and then feed that result
to `newk`.  This is just an accumulator recursion, but what we are accumulating now is
a function, or a computation.

So far, so good; the magic happens on line 3, when we find a 1 in the list.  Instead of
calling `aux` recursively or using `newk`, we call the top-level continuation `k` instead.
This bypasses all the computations that were in `newk`.  No calls to `gcd` will happen at
all in this scenario, and the auxiliary function will abort as soon as it finds a 1 in the list.

We have basically implemented exceptions using only pure functions.

## Slide 12 - Other Topics

In addition to simulating exceptions, continuations can simulate multitasking.  When they
are used like that they are called *co-routines*.  There are also more advanced versions
of continuations, called *delimited continuations*.  They have names like *shift* and *reset*.
Finally, some languages, notably Scheme, allow you to capture the continuation of a running 
program with a command called `call/cc`.

I hope this gave you a good introduction to continuations.  In the next video we'll show
you how to transform a program written in direct style into continuation passing style.

