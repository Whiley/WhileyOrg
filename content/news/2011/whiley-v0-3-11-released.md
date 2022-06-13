---
date: 2011-10-28
title: "Whiley v0.3.11 Released!"
draft: false
---

As usual, it's been a surprising amount of effort ... but the next release of Whiley is available!  It's been quite a long time since the last update, but then quite a lot has improved.  Unfortunately, I did find a fairly serious problem with my type system, which means I've got to go back to the drawing board and figure out how to fix it.
## ChangeLog

   * Fixed support for line numbers in classfiles (this required adding dead-code elimination phase at the WYIL level)

   * Added a generic class for handling error messages.  The aim here is improve the quality and consistency of error message reporting, by providing a central class which is responsible for this.  However, this is in its infancy and a lot remains to be done here.

   * Improved Compiler Documentation.

   * Added support for parsing and checking throws clauses.  This require extending the function and method types to include another slot for the throws clause, which behaves much like that for return values.

   * Added support for checking that catch handlers are not dead-code.  That is, every catch handler must be able to catch something in the try-catch block.

   * Added support for the `native` modifier on functions/methods.  This indicates that the given method is implemented as a native Java method.  Under-the-hood, such methods are redirected into a class of the same package and name (but with "$native" appended to the name).

   * Added support for the `export` modifier on functions/methods.  This tells the compiler that the function or method in question is intended to be called by some external (i.e. native Java) code.  Thus, the compiler omits the usual name mangling it would apply.

   * Added support for passing modifiers (including native and public) through into the WYIL (which was surprisingly absent).

   * Changed the way cases of a switch statement work.  Now, you can no longer "[fall-through by default](http://whiley.org/2011/10/26/fall-through-by-default-switch-statements/)".

   * Removed the implicit coercion from `char` to `int`, which really didn't make sense.  You can still force this coercion using an explicit cast.

   * Added some more methods to the core standard library.

   * Added support for testing the length of a dictionary.

   * Added `do` - `while` statement.

   * Fixed a lot of bugs!

## Future Work

   * Fix the problem with type difference, where currently `[int] - [int] => [void]`

   * Back propagation doesn't work properly for try-catch blocks

   * Back propagation doesn't work through pre-/post-conditions and loop invariants.

   * Many of the type constraints are not expanded properly.

   * Include support for e.g. *effective* list types, etc.

   * There is currently no way to determine if when a dictionary contains a particular key.
