# Assignments

We will have two assignments early on.
These assignments can be implemented in any programming language(s).
(We have done them in the Scala, Python and Scheme.)

## _BUS_: Bottom-Up Search

_BUS_ is the non-ML subset of [_BUSTLE_](https://arxiv.org/abs/2007.14381).

Your task is to implement bottom-up enumerative search for simple compound expressions, excluding conditionals, recursion and loops.

You can pick your own target language(s) as well.
Your implementation should be generic and support more than one target language.
For example, when I (Prof. Amin) did this assignment, I picked two target languages: a subset of Scheme and the FlashFill-like string manipulation DSL used in the _BUSTLE_ paper.

If you'd like to look at the test data that I used for the two target languages, they are here.

### [Test data](data/bottomup.scm) for the Scheme subset

Each data entry is of the form

```(<name> (<arg> ...) (((f <input> ...) <output>) ...) <solution>)```

Each data entry comes from _Dan_ (see the **next** assignment below) delegating a subcase to _BUS_.

For example, here are the two data entries for `filter`, a function that takes a predicate and a list, and returns a list of only the elements in the input list satisfying the predicate. There are two recursive cases to consider in the definition of filter: when the first element of the list does not satisfy the predicate, in which case it is discarded (right-hand side solution `?rec`), and when the first element of the list satisfies the predicate, in which case it is kept (right-hand side solution `(cons (car xs) ?rec)`).

```
 (filter
   (?rec p xs)
   (((f '(4 2) even? '(3 4 2 1)) (4 2))
     ((f '() even? '(1)) ())
     ((f '(2 1) (lambda (x) (not (= x 0))) '(0 2 1 0)) (2 1))
     ((f '() (lambda (x) (not (= x 0))) '(0)) ()))
   ?rec)

 (filter
   (?rec p xs)
   (((f '(2) even? '(4 2 1)) (4 2))
     ((f '() even? '(2 1)) (2))
     ((f '(2 1) (lambda (x) (not (= x 0))) '(3 0 2 1 0)) (3 2 1))
     ((f '(1) (lambda (x) (not (= x 0))) '(2 1 0)) (2 1))
     ((f '() (lambda (x) (not (= x 0))) '(1 0)) (1)))
   (cons (car xs) ?rec))
```

### [Test data](data/bottomup.txt) for the string manipulation DSL.

### Hints

Note that the bottom-up search requires both the syntax and semantics of the target language.
For example, if you have an expression language, you might have a grammar rule `e -> e + e` and a semantic rule to compute the addition given the values of two expressions.

## _Dan_: Synthesizer of Recursive Functions

_Dan_ writes recursive functions in the style taught by Daniel P. Friedman (_The Little Schemer_, _The Little Learner_).
_Dan_ calls _BUS_ to solve cases, both base cases and recursive cases.

Your task is to handle more complex expressions than in your previous assignment, for example involving conditionals, loops and recursion.

One approach is _Dan_. You may devise any approach inspired by the literature.
