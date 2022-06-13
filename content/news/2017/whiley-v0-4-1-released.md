---
date: 2017-08-03
title: "Whiley v0.4.1 released!"
draft: false
---

The next release of the Whiley Development Kit is upon us.  This is about six months since the last official release and, in the meantime, a lot has been going on!  For example, there have been more than ten releases of the Whiley Compiler (WyC) itself on [Maven central](http://search.maven.org/#search%7Cga%7C1%7Cwhiley).  The main updates are:
   * **RFCs**.  A new process for proposing language changes (RFCs) has been instigated (see [here](https://github.com/Whiley/RFCs/)).  This is done by submitting a pull request to the official RFC repository.  Currently, there are eight accepted RFCs and several more in the pipeline.

   * **Standard Library**.  The standard library has now been refactored roughly in line with [RFC#0007](https://github.com/Whiley/RFCs/blob/master/text/0007-refactor_stdlib.md).  This changes the structure from e.g. `whiley.lang.*`  and `whiley.io.*`  to a single package structure `std.*` .  This makes the library easier to digest, and more in line with other systems languages (e.g. C++, Rust, D).

   * **Language**.  Numerous improvements and bug fixes have been implemented in the Whiley Compiler (WyC).  Examples include: type invariants are now properly enforced (see [#751](https://github.com/Whiley/WhileyCompiler/issues/751)); Syntax for property declarations has been added (see [#711](https://github.com/Whiley/WhileyCompiler/issues/711)); Syntax for named record initialisers has been added (see [#704](https://github.com/Whiley/WhileyCompiler/issues/704)).

   * **Verification.**   Numerous significant improvements to the Whiley Theorem Prover (WyTP) have been implemented.  It has essentially been rebuilt from scratch and, as a result, both performance and coverage are significantly improved.  A mechanism for showing generated *proofs*  has been added. Furthermore, there is now rudimentary support for generating *counter examples* .

   * **Command-Line Tool**.  The command-line tool, `wy` , has been updated with better support for displaying help information.  See [here](http://whiley.org/about/getting-started/) for some information on using it.

   * **Experimental Backends**.  Two new experimental backends have been included in this release.  The first is for generating *Javascript*  and the second for generating *Java source* .  Whilst these are not complete, they are still useful (particularly the Javascript backend).

   * **Whiley Language Specification**.  This has been updated with more information regarding the process of definite assignment checking, and type checking.


The next major improvements include an overhaul of the WyIL API used within the compiler, and implementing some or all of the outstanding RFCs.  Also the introduction of a proper package manager and build system.  Work will also be continue on improving verification.
