---
id: The CPS Transform
aliases: []
tags: []
---


<iframe id="kmsembed-1_5bs7ap1s" width="640" height="394" src="https://mediaspace.illinois.edu/embed/secure/iframe/entryId/1_5bs7ap1s/uiConfId/55779922/pbc/113245372/st/0" class="kmsembed" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" referrerPolicy="no-referrer-when-downgrade" sandbox="allow-downloads allow-forms allow-same-origin allow-scripts allow-top-navigation allow-pointer-lock allow-popups allow-modals allow-orientation-lock allow-popups-to-escape-sandbox allow-presentation allow-top-navigation-by-user-activation" frameborder="0" title="The CPS Transform"></iframe>

## Slides
- [[05.1.2-cps-transform.pdf|The CPS Transform (PDF)]]

# CPS Transform Transcript

## Slide 1 - Title

Hello everyone, and welcome to CS 421.

In the last video you saw some examples of writing functions in continuation
passing style.  Now we are going to treat this more formally and give you an
algorithm to convert a function from direct style to continuation passing
style.

## Slide 2 - Objectives

Once you are done with this video, you will be able to use the formal definition of a CPS transform to do the transformations.

Before we get started, there is something I'd like to let you know. There are
many different kinds of CPS transforms, and if you check elsewhere you are
likely to find many different versions. Some CPS transforms convert every
subexpression, even those that do not actually need to be converted, and makes
the result kind of cluttered. The version we will go over here distinguishes
between terms that need to be rewritten into CPS and those that do not, and I
find that it tends to produce results that look like the kind you would have
gotten if you wrote the function in CPS directly.

## Slide 3 - The CPS Transform, Simple Expressions

To represent the CPS transform, we will use the capital letter C and put
the term we are transforming in the semantic brackets.  There are four
situations we have to consider.

The first thing we need to do to convert a function is to create a new variable
k and add it to the function's parameter list.  You can actually name it anything
you want, as long as the variable name is "fresh", that is, is not already used
in the function.

Once we have done that, we transform the body of the function.  Notice that the
`k` is a subscript now.  This indicates to our transformer function what the
current continuation is.

The second situation is transforming simple expressions.  An expression is simple
if there are no function calls that could be activated in the code.  The main
way a function becomes unavailable is if it is inside a lambda expression that
does not get called. 

If there are no function calls (at least, none that matter), we can simply pass
the expression to the current continuation and be done.

Here are a few examples.  Notice that each of these function bodies just
return a constant.  In direct style we would return these, but in CPS we pass
them to the current continuation.

Hit pause and try converting these to CPS.  The answers are on the next slide.

(PAUSE)

## Slide 4 - Simple Expression Examples

Okay, here are the results.  All we had to do is add a continuation argument
to each function's parameter list, and then pass the body of each function
into its continuation argument.

(PAUSE)

## Slide 5 - The CPS Transform, Function Calls

There are two other cases to look at, and both involve function calls.

In the first case, we have a function applied to a simple argument `arg`. We
assume that `f` is also written in CPS. This means that `f` cannot return a
value, but instead needs to be given a continuation argument, so we give it the
one we have, written as `k` here. If `f` happened not to be in CPS, then we
would treat the whole thing as a simple expression and use the previous rule to
translate it.

I should mention here, this rule is written as if $f$ has already been
processed.  If $f$ is a lambda expression, the rule would need to be a bit
more complex.  We won't cover that case in this lecture.

The last case is the tricky one.  In this case, the argument $arg$ is
itself going to be transformed into CPS, and will therefore need a
continuation argument.  We can't simply pass its value into the function
$f$, so we will have to build a continuation to capture the result of
evaluating it.  That continuation can then pass the result into f.

The new continuation starts with a $\lambda v$, where $v$ is a variable
we have not used before.  We feed $v$ to $f$, and then pass the current
continuation $k$ to $f$ as well.

Here is a function for you to try converting.  Hit pause and resume when
you are ready to see the answer.

(PAUSE)

## Slide 6 - Example

Here is the result. You can see all four of the rules in play here, in the
second listing. The first rule says to add a continuation argument to each of
the function declarations. The second rule is for simple expressions, and we
used that on line 1. The third rule is for function calls with simple arguments,
which we used on line 2, and the last rule is for expressions where the
argument is not simple, that is it needs its own continuation.  You can see
this on line 3.

## Slide 7 - Operators

If you have an operator, there are three cases.  It could be that both
arguments to the operator are simple.  In that case, the whole thing is
simple and we can pass it all into the current continuation.

If one of the arguments is not simple, we transform it and pass in a
continuation that captures its result and uses that to perform the
operation.  The rule shows $e_1$ here.  The $e_2$ case is symmetrical
to this one.

If both arguments need continuations, we first call the transformed $e_1$ and
capture its result in $v_1$.  Next we call the transformed $e_2$ and
capture its result in $v_2$.  We can finally apply the operation to $v_1$
and $v_2$ and pass the result into the current continuation.

This makes a nested continuation.

## Slide 8 - Examples

Here are some functions for you to try converting.  Pause the video and
try converting them, and resume when you are ready to see the answers.

(PAUSE)

### `foo`

For `foo` we have a simple expression, so we just need to pass it into
the current continuation.

(PAUSE)

For `bar` the first argument needed to be converted.

(PAUSE)

For `baz` we converted the second argugment.

(PAUSE)

And finally for `quux` we have to convert both of them.


## Slide 9 - References

There are a lot of research papers written about continuations and
continuation passing style.  Here are a few of my favorites.
The first two are a bit technical, and the last one gives a nice
overview of all the times someone discovered this way of programming.

