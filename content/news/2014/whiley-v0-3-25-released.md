---
date: 2014-06-09
title: "Whiley v0.3.25 Released!"
draft: false
---

Time for another release of the Whiley compiler. This is relatively low key, though includes the first steps towards an improved bytecode API (see {{<issue id="190">}}). There are also a range of bug fixes for various minor issues:

   * Refactoring `wyil.lang.Code` and `wyil.lang.CodeBlock`.  In order to support proper nested bytecode blocks, I am refactoring the WyIL bytecode API.  This will allow a `Block` to nested within another `Block`.  The main advantage of this is from a usability perspective, as it will eliminate the `LoopEnd` bytecode which has proven problematic.
   
   * Fixed bug {{<issue id="352">}} which was a problem with the verifier.

Recently, I have been making relatively slow progress on the compiler.  This is because I have been distracted writing grant applications and teaching; I've also been working on the [Whiley Language Specification](https://github.com/Whiley/WhileyDocs/tree/master/WhileyLanguageSpecification) as well.  Whilst I still have a few more administrative things to sort out, I'm hoping to put more time into the compiler in the near future.  My current goal is to complete a full pass through the `wyil` module, improving the overall design, refactoring code and adding more documentation.  Following this, the next goal is to complete the [plugin framework](https://github.com/Whiley/WhileyCompiler/issues?direction=desc&milestone=22) (which I have also been working on already).
