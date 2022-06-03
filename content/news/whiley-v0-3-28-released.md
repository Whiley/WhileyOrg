---
date: 2014-08-22
title: "Whiley v0.3.28 Released!"
draft: false
---

The next release of Whiley is already upon us, after only a week or so since the last.  This release consists of a slew of minor bug fixes, many of which have been discovered through students using the system in practice.  The main items are:
   * **Problem Generating JVM Bytecode** ([#415](https://github.com/Whiley/WhileyCompiler/issues/415)).  This related to compiling functions or methods that used large numbers of local variables (i.e. more than 255).

   * **Definite Assignment Checking for Records** ([#408](https://github.com/Whiley/WhileyCompiler/issues/408)).  The definite assignment checker was not correctly spotting assignments to uninitialised compound structures (e.g. records).

   * **Missing Return Statements** ([#395](https://github.com/Whiley/WhileyCompiler/issues/395)).  The compiler was not checking for missing return statements in all cases, which was leading to confusing error messages.

   * **General Verifier Bugs** ([#400](https://github.com/Whiley/WhileyCompiler/issues/400), [#401](https://github.com/Whiley/WhileyCompiler/issues/401), [#403](https://github.com/Whiley/WhileyCompiler/issues/403), [#404](https://github.com/Whiley/WhileyCompiler/issues/404), [#405](https://github.com/Whiley/WhileyCompiler/issues/405), ). There were a range of bugs within the verifier itself which are now fixed.


There are more improvements in the pipeline, particularly related to performance of verification condition generation which is currently a key bottleneck for verification (see [#377](https://github.com/Whiley/WhileyCompiler/issues/377)). 
