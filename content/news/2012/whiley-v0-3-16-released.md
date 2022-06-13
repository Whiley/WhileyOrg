---
date: 2012-07-31
title: "Whiley v0.3.16 Released!"
draft: false
---

Well, after a reasonable wait, the next release of Whiley is finally upon us.  This represents a number of fairly significant changes, all of which  improve the compiler very nicely.
## ChangeLog

   * The Whiley Intermediate Language (WYIL) is now a *register-based* bytecode language, rather than a *stack-based* one.  This offers a number of nice improvements to the compiler.  In particular, it simplifies several stages (e.g. constant propagation) which no longer have to be concerned with maintaing stack consistency.

   * The Whiley Intermediate Language (WYIL) now has a binary file format.  This may seem unimportant but, in fact, it opens up a number of significant improvements to the compiler.  In particular, the build system can now correctly support multiple back-ends simultaneously; constraints and encapsulation modifiers can be extracted from e.g. library function calls (where previously they were being lost); we could now (in principle) write a standalone interpreter for WYIL bytecodes; we can now independently compile from Whiley to WYIL and then from WYIL to some other architecture; finally, it should be relatively easy now to fix the problem of "horizontal dependencies" during incremental compilation (which is particularly important for the Eclipse plugin).

   * The Whiley Development Kit has been completely reorganised.  This is largely thanks to the WYIL binary format, which has enabled me to properly isolate the separate modules.  Thus, WYIL forms the core module and everything else builds of this.

   * The notion of a "message" has now been completely stripped out of the compiler.  There are now only functions (which are pure) and methods (which may have side-effects).

   * The assume statement has been added.  This differs from the assert statement in that the verifier will not fail with an error if the assumed condition cannot be shown to hold.  Instead, the verifier will simply "assume" that the condition does hold.

   * The amount of redundant code that existed between the Ant tasks and the Main classes which were previously used solely from the command-line has been reduced by factoring it out into a generic "build task".  This may also be useful for the Eclipse plugin, although at this stage it's unclear.

   * Numerous bugs have been fixed, including a few which have been lurking unnoticed for some time.
