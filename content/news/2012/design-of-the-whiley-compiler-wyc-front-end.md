---
date: 2012-02-13
title: "Design of the Whiley Compiler (Wyc) Front-End"
draft: false
---

Designing the front-end of the Whiley Compiler (Wyc) is a somewhat delicate and complicated issue.  I have iterated on this a few times, and still not found a solution I'm happy with.  It's important, because it ultimately determines what is possible in terms of language syntax and what is not.  That is, when certain events occur in the front-end determines whether or not I can pull off certain "tricks" to simplify my syntax or not.

In an effort to help me get a good handle on the problem, I'm going to try and enumerate the main issues here.  With any luck, the answer will just pop out ...
## Overview
The main task of the front-end is to convert Whiley source code into the Wyil intermediate bytecode.  The key aspects of Wyil are:
   * Wyil is an unstructured intermediate language, whose programs are composed of bytecodes (similar in many ways to Java Bytecode).

   * All names used in Wyil bytecodes are fully resolved (i.e. they include appropriate package and module identifiers).

   * All Wyil bytecodes are associated with an appropriate type.  For example, the type of a `length` bytecode must be an effective collection (i.e. an effective list, set, dictionary or string).

   * All constraints should be expanded (or, at least, partially expanded)


As an example, consider this Whiley program for summing a list of naturals:

```whiley
import nat from whiley.lang.Int

public int sum([nat] list):
    r = 0
    for i in list:
        r = r + i
    return r
```

This is compiled into the following Wyil bytecodes:

```whiley
public int sum([int] list):
requires:
    load 0 : [int]
    forall 2 : [int]
        load 2 : int
        const 0 : int
        ifge goto exitlab : int
        fail "constraint not satisfied"
    .exitlab
body:
    var r, i
    const 0 : int
    store r : int
    load list : [int]
    forall i : [int]
        load r : int
        load i : int
        add : int
        store r : int
    load r : int
    return : int
```

We can see that the type `nat` has been expanded to `int` by looking at its definition in `whiley.lang.Int`.   The requires clause represents the expanded constraints generated from `[nat]` --- namely, that every element of `list` should be non-negative.
### Resolution
An important aspect of converting Whiley source into Wyil is *resolution*.  This is about determining what a given name in a source file actually corresponds to by looking it up in the WHILEYPATH following the given import statements.  As part of this, types and constants must be expanded into fully resolved types and constants.  For example, consider this:

Light.java:

```whiley
define Light as {
  Point point,
  Colour colour
}

...
```

Scene.java:

```whiley
import Light

define Scene as {
 [Light] lights,
 [Object] objects
}

...

private Colour colourAt(Light light, Point pt):
   ...
```

In order to fully resolve the type `Scene`, we must resolve the type `Light`.  This involves, firstly, determining what module `Light` is defined is (by following the `import` trail) and, secondly, what `Light`'s fully resolved type is.  Similarly, we must trawl the source code of functions (e.g. `colourAt`) and resolved any names referred to (in this case, the type of parameter `light`).

Resolution is an inherently global task, since types obviously may be defined in terms of types in other modules.  Furthermore, types may be recursive across modules and modules may have dependencies going in both direction (e.g. type `X` in one module refers to type `Y` in another, whilst type `Z` in the latter refers to a type in the first, etc).
### Flow Typing
The second major task faced in converting Whiley source into Wyil bytecodes is that of *flow typing*.  This is the process of determining a type for every expression and statement in the program, including all intermediate expressions used.  During this process some ambiguity between different expressions with the same syntax will be resolved (e.g. `x+y` can be either arithmetic addition, or set union --- and we can only determine this when we know the types of `x` and `y`).

Looking at a similar example to before, we can see roughly how flow typing proceeds:

```whiley
real sum([real] list):
   r = 0           // r => int, based on type of constant 0
   for v in list:  // v => real, based on type of list
      r = r + v   // r => real, based on type of operands
   return r       // r => real|int, based on type of r after loop
```

The key difficulty with flow-typing is that is an inherently flow-sensitive activity, which is particularly problematic in the presence of exceptions and retyping expressions (i.e. those involving `is`).
## Two Differing Approaches
One of the key design issues in the compiler front-end is the choice of when to convert from the source-level AST into the Wyil bytecodes.  There are essentially two main approaches:
   * **(Late-Generation)** Here, flow-typing is performed directly on the AST which is subsequently converted into Wyil bytecodes.

   * **(Early-Generation)** Here, the AST is first converted into temporary Wyil bytecodes which are then flow-typed to produced the final bytecodes.


For some reason, the choice of which approach to take has caused me a lot of headaches.  I believe either can be made to work.  The issue, of course, is in finding the simplest most coherent approach.  This always seems to save me time in the long run.  One reason for this is that generation is intertwined with *constraint expansion* (that is, generating Wyil bytecodes corresponding to source-level constraints).  The main trade-offs are:
   * **Late-Generation. ** This is probably the most logical approach.  However, it is harder to properly flow-type the AST because of retyping (i.e. `is`) expressions.  On the other hand, there is potential to support retyping of complex retyping (e.g. involving records and possibly lists).  This approach also requires an awkward abstraction which I refer to the as "unconstrained types".

   * **Early-Generation.** This is awkward because it requires special abstract bytecodes to encode ambiguous expressions which can only be resolved when types are known (the trickiest being related to the various kinds of method invocation).  However, flow-typing is much simplified because it operates on the unstructured intermediate language where flow-sensitive analysis is easier.  There is also no need to support the notion of an "unconstrained type".  Another downs-side of this approach is that it relies on Wyil bytecodes being able to encode nominal types.  However, I want to support this anyway in order to simplify debugging Wyil code.


The issue of unconstrained types is slighty odd.  It stems from a separation from expanding types and expanding constraints.  For example, consider this:

```whiley
define nat as int where $ >= 0

int f(nat|[int] x):
    if x is nat:
        return 0
    else:
        return |x|
```

Currently, this program should (in fact) fail compilation because `x` must have type `int|[int]` on the false branch.  The notion of unconstrained types handles this by replaced all constrained types with `void` before computing the type difference on the false branch.  If the constrained was expanded before type checking this function, then there would be no need for an unconstrained type as it would be implicit.  Things get particularly awkward when we consider types in compiled libraries, since one cannot retro-actively determine the unconstrained type.  Instead, for every type, we'll have to embed the unconstrained version as well.

Ok, that's it for now.  I'm not sure how much this is helping me, but I probably need to add more of the subtle trade-offs as I remember them.
