---
date: 2014-05-07
title: "Whiley v0.3.24 Released!"
draft: false
---

Well, it's time for yet another release of the Whiley compiler.  This one is fairly low key, focusing primarily on bug fixes.  Specifically, these issues have been resolved:
   * [#346](https://github.com/Whiley/WhileyCompiler/issues/346) --- *Temporary Fix for Unsuported Bytecodes in the Verifier.*

   * [#341](https://github.com/Whiley/WhileyCompiler/issues/341) --- *Temporary Fix for Verifying Method Types.*

   * [#338](https://github.com/Whiley/WhileyCompiler/issues/338) --- *Fix for handling record constants in the Verifier.*

   * [#345](https://github.com/Whiley/WhileyCompiler/issues/345) --- *Fix for handling of loop variant variables in the Verifier.*


I have also been through the test cases which are currently failing verification, and classified most of them.  In quite a few cases, this resulted in yet more issues being added to GitHub.  An example of an interesting issue I found is the following:
   * [#343](https://github.com/Whiley/WhileyCompiler/issues/343) --- *Problem Verifying Do/While Loops.*


Finally, I also made progress towards two current milestones: the [plugin system](https://github.com/Whiley/WhileyCompiler/issues?milestone=22&state=open), and [nested WyIL bytecode blocks](https://github.com/Whiley/WhileyCompiler/issues?milestone=15&state=open).  As usual, you can get the latest files below.  Furthermore, you can now run Whiley in your browser from [here](http://whiley.org/play/), whilst the [Eclipse plugin](https://github.com/Whiley/wyclipse) will be updated in the near future.
