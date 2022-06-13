---
date: 2010-07-10
title: "Whiley v0.2.8 Released!"
draft: false
---

Here is the latest update for the Whiley-to-Java Compiler.  It now weighs in at around 47KLOC, spread over 272 classes.  There are 379+ distinct test inputs, which give rise to around 615 actual JUnit tests.  Anyway, the list of improvements includes:
   * Fixed numerous outstanding bugs

   * Improved reporting of syntax errors

   * Added list append

   * Added support for recursive types

   * Added the type matching operator ~=

   * Modified syntax of define.  Instead of "define type where cond as name", it's now "define name as type where cond"

   * Small updates to standard library

   * Redesigned the way Wyone handles types to enable better translation of Whiley's union types


Overall, it's looking a lot better.  However, it still won't compile anything that's really non-trivial and there are several outstanding design flaws that need to be figured out.  These include:
   * The way constrained recursive types are handled is insufficient.  The problem is that recursive types are handled using a recursive type constructor (e.g. X[int | (X left, X right)]) , but there is no equivalent for the constraints.  One possible solution here is a closer coupling between the type itself and the constraints imposed upon it.

   * The way type tests are implemented does not work well with type inference.  Type inference is used to prevent the need for a cast operator in Whiley.  The problem is when you perform a type test on something which is not a variable, then we cannot update the environment to reflect this.  One possible solution here is to introduce a simplified intermediate representation which uses a 3 address code.  This would then mean complex expressions where broken down into simpler ones which were connected via conditional branching.

   * The way boolean values are represented in the automated theorem prover, wyone, does not work well.  Wyone currently follows a classical approach where we things which return boolean values have a special status.  For example, a predicate is a special kind of function which returns a boolean.  The disadvantage of this is that it makes things rather unsymetric, and is responsible for a number of outstanding bugs.  A more unified, albeit less classical, approach would considerably simplify things.


Right, that's all fow now --- enjoy!
