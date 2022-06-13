---
date: 2015-06-05
title: "Whiley v0.3.34 Released!"
draft: false
---

Finally, after almost two months of effort, the next version of Whiley is released.  This release has taken a long time, not because it contains so much, but simply because I have been truly busy with teaching my second year paper SWEN221.  Nevertheless, this release does contain some interesting additions:
   * **Refactored Test Cases**.  The valid test cases have been refactored to avoid relying on sample output.  Instead, each test case simply uses `assert` and `assume` statements to ensure certain properties are true.  This is helpful for a number of reasons.  In particular, it significantly reduces reliance on the standard library which is part of my plan to split out the standard library from the compiler itself.  The test cases have also refactored to reduce other dependencies on the standard library, although more work is needed on this.

   * **Bytecode Interpreter**.  An interpreter for WyIL bytecodes (`wyil.util.Interpreter`) has been developed which allows execution of Whiley programs without relying on the JVM backend.  This is also part of my plan to split out the compiler into a collection of plugins, consisting of the main compiler from Whiley source to WyIL bytecodes and then different plugins implementing different backends (e.g. to JVM bytecode).

   * **Various Bug fixes**.  A small number of additional bugs have been fixed (see [#487](https://github.com/Whiley/WhileyCompiler/issues/487) and [#488](https://github.com/Whiley/WhileyCompiler/issues/488)).
