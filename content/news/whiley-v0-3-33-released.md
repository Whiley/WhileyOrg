---
date: 2015-04-08
title: "Whiley v0.3.33 Released!"
draft: false
---

The next release of Whiley is upon us!! Work got a little bogged down with the start of term, but should hopefully now pick up a little.  The main component of this release is the removal of the `string` and `char` data types from the language. This is quite a big change, but is in line with my efforts to simplify the language. Instead of `string`, we now simply have a list of integers. Furthermore, we can constrain these integers to be, for example, ASCII or UTF8, etc.
   * **Removed string and char data types ([#432](https://github.com/Whiley/WhileyCompiler/issues/432))**.  As discussed above, this is a fairly large change.  In particular, it required updating a large number of the test cases and benchmarks.

   * **Removed protected modifier ([#448](https://github.com/Whiley/WhileyCompiler/issues/448))**. The protected modifier was not really implemented and, although it's a good idea, for now I've left it out.  This is something to be scheduled for proper inclusion down the track.

   * **Removed WyIL Method / Function Cases ([#475](https://github.com/Whiley/WhileyCompiler/issues/475))**.  Method / function cases were originally included to support overloading on pre- and post-conditions.  However, this hasn't been supported for a long time now.  Furthermore, with the advent of proper nominal type information at the WyIL level, we can get a very similar effect by using named types.

   * **Removed implicit imports ([#479](https://github.com/Whiley/WhileyCompiler/issues/479)).** Following Java, I originally chose to have the package `whiley.lang.*` implicitly imported in every source file.  However, this exception was clearly a bad idea, not least because I want to imagine Whiley programs which are not necessarily connected with the standard library.  Therefore, this is removed and all test cases and benchmarks have been updated.

   * Improved Error Messages for Loop Invariants ([#486](https://github.com/Whiley/WhileyCompiler/issues/486)). Prior to `v0.3.32`, error messages were being reported correctly for loop invariants.  However, with the introduction of the `Invariant` bytecode, some issues arose and I resorted to a temporary fix for reporting error messages.  This is now fixed.


In addition to these updates, I've also been through and updated the [Whiley Language Specification](http://whiley.org/pdfs/WhileyLanguageSpec.pdf) and the [Getting Started with Whiley](http://whiley.org/pdfs/GettingStartedWithWhiley.pdf) tutorial accordingly.  All up, this release is definitely an improvement over `v0.3.32`, although there is still a way to go before things are properly back on track. 
