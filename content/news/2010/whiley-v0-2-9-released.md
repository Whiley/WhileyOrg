---
date: 2010-07-25
title: "Whiley v0.2.9 Released!"
draft: false
---

Well, here's version 0.2.9.   This includes numerous bug fixes, and several major feature updates:
   * Support for recursive algebraic datatypes

   * Improved support for type testing, particularly of recursive types

   * Syntax of function declarations has changed slightly to use `where` instead of `requires` + `ensures`.  See [this post](http://whiley.org/2010/07/23/thinking-about-pre-and-post-conditions-in-whiley/) for more on why.


However, there remains a long list of outstanding issues:
   * Compile-time checking of recursive constrained types is a problem in some cases.  See [this post](http://whiley.org/2010/07/25/thinking-about-recursive-constrained-types-in-whiley/) for more.

   * Type inference doesn't work in all cases either.

   * Boolean lists remain a problem.


At this stage, I am faced with some difficult choices.  The current design is getting overly complex and, frankly, I don't believe it will go the distance.  A new design is really needed that will dramatically simplify many aspects of the process.  My current thinking on this is to move towards a simplified [intermediate language](http://wikipedia.org/wiki/intermediate_language), similar in some ways to [Java bytecode](http://wikipedia.org/wiki/Java_bytecode).  The advantage of this is that it would significantly reduce the number of cases that need to be processed; it would also provide a nice interface between the front-end and the back-end, helping to separate them and improve overall modularity.
