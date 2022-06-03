---
date: 2010-06-24
title: "Whiley v0.2.7 Released!"
draft: false
---

Well, finally, after a lot of effort I have a new release of the Whiley Development Kit.  To get it, follow the download links on the left.

The major difference over the previous version is that the theorem prover has been almost completely rewritten.  So, while on the surface it might not appear much different, under the hood it certainly is!  The upshot is that it's now correctly passing quite a few more examples.  The theorem prover is also capable of generating models for integer, real and tuple values (but not for lists and sets yet).  At the moment, the compiler doesn't exploit this to enable the three-valued logic where constraints it can't prove either way are turned into runtime checks.  This should follow pretty soon now though.

Anyway, the list of known issues remains long, and includes:
   * List append is not implemented.

   * Non-unicode versions of some operators are not implemented (e.g. set union, subset, etc).

   * Module modifiers (e.g. public/private etc) are not implemented.

   * Imperative looping constructs (e.g. while/for) are not implemented (can use recursion instead)

   * Processes have relatively poor support; they are properly threaded, and there remain various issues related to reasoning about them.

   * The print statement still exists (this will be deprecated in favour of a "debug" statement, which will only be used in debug compiles)

   * Various aspects of the syntax remains to be changed (e.g. define will have name first, then details; functions/methods will use where instead of requires/ensures).

   * Maps are not implemented.

   * The theorem prover still has some issues with handling lists/sets (although many cases do work well)


Anyway, there's probably more I haven't thought about!  But, we're definitely moving in the right direction ...
