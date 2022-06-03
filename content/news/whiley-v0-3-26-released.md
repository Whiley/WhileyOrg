---
date: 2014-07-25
title: "Whiley v0.3.26 Released!"
draft: false
---

It's about time for another release of Whiley.  This represents some interesting developments, though I continue to struggle with debugging and improving verification.  The main highlights for this release are:
   * **Improved `wyal` file parser**.  This is responsible for parsing `wyal` files and feeding them into the code generator.  Previously, the parser was very simplistic, and was neither extensible nor correct (in some cases).  Therefore, I have pulled out a lot of stuff from the very nicely written `WhileyFileParser` and adopted a similar style.  I have also made some minor refactorings to the AST represetantion of `wyal` files.

   * **Improved Quantifier Instantiation Algorithm**.  For various reasons, the above change forced me into finally working on improving quantifier instantiation.  To do this, I have created a native WyRL function which handles binding and trigger search.  This works well within the confines of how it was designed; however, there are still a number of hurdles to overcome related to verification (see [#373](https://github.com/Whiley/WhileyCompiler/issues/373),  [#375](https://github.com/Whiley/WhileyCompiler/issues/375) and [#379](https://github.com/Whiley/WhileyCompiler/issues/379)).

   * **Fixed outstanding bug with WyRL Automata**.  To my complete disbelief, there was an outstanding critical bug in the equivalence matching of automaton.  I am amazed this bug survived for so long without being noticed.  I demonstrated the bug was realisable, and have corrected it (see [#374](https://github.com/Whiley/WhileyCompiler/issues/374)).  I didn't find any test cases which now passed as a result though, which was disappointing.

I'm now working specifically on improving issues related to quantifier instantiation in order that a bigger range of examples involving non-trival loop invariants will pass.
