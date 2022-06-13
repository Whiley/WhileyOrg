---
date: 2014-02-15
title: "Whiley v0.3.22 Released!"
draft: false
---

The next release of Whiley is now available. This implements some significant changes to the language syntax, as discussed in [this post](http://whiley.org/2013/12/19/proposed-syntax-changes-for-whiley/) and [this post](http://whiley.org/2014/01/23/thoughts-on-parsing-whiley-and-indentation-syntax/). Although the migration towards this new syntax is not fully complete, it is largely working well. Specifically, the main changes in this release are:
   * **Draft Language Specification**.  Perhaps one of the most important additions to the Whiley system is an early draft of the *Whiley Language Specification*.  This document can be obtained online [here](http://whiley.org/Documentation), and provides the most comprehensive account of the language to date.  Over the coming months, this will be further fleshed out to give a complete account of the language.

   * **Whiley Parser Rewritten**.  To implement the new syntax and to make the language more robust to variations in the use of whitespace (e.g. for multi-line expressions), the parser was rewritten from scratch.

   * **Front-end refactored**.  The front end of the compiler is responsible for parsing and type checking Whiley source files, as well as performing WyIL code generation.  The structure of this was previously somewhat incoherent, and I've made significant efforts to improve this and more code comments.

   * **Build-system refactored**.  The build system has been refactored into three modules: the *Whiley File System (WyFS)*, the *Whiley Build System (WyBS)* and the *Whiley Compiler Collection (WyCC)*.  This is partly to improve coherence of the code, and partly in preparation ahead of splitting up the compiler to use a plugin system.  Additionally, the build system was reworked to support the generation of multiple binary files from a single source file (this was needed for properly implementing lambdas in the JVM backend).

   * **Whiley Standard Library refactor**.  The standard library has been ported to the new language syntax and also refactored so that `File.Reader` actually implements `Reader` (finally).

   * **Visibility Modifiers Implemented**.  The visibility modifiers (i.e. `public`, `private`, `protected`) have properly implemented now (at last).

   * **Implementation of Lambdas on the JVM reworked**.  The implementation of lambda's on the JVM has been reworked to avoid using reflection.  This was necessary to support visibility modifiers.


Overall, I am very pleased with this release as it represents a lot of improvements to the language.  In terms of the new syntax, the following are the major outstanding pieces yet to be implemented:
   * **Flow Typing ignores Declared Type**.  Currently, the flow type checker ignores the declared type of a variable.  This means that you can currently assign a declared variable a value of any type!

   * **Verification ignores Declared Type**.  Currently, the verifier ignores the declared type of a variable and, in particular, any invariants implied by this type.  Therefore, you cannot currently use the declared type of a variable to enforce an invariant for the lifetime of a variable.


The above will hopefully be fixed in the near future.  As usual, you can get the latest files below.  Furthermore, you can now run Whiley in your browser from [here](http://whiley.org/play/), whilst the [Eclipse plugin](https://github.com/Whiley/wyclipse) will be updated in the near future.
