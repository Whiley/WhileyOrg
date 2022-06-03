---
date: 2015-12-17
title: "Whiley v0.3.37 Released!"
draft: false
---

Another big update to Whiley landed today, and includes a whole raft of changes. In particular, various algorithms in the automated theorem prover have been reworked to improve performance (though more still needs to be done here). A rough summary of the changes in this version is:
   * **Performance Improvements for Automated Theorem Prover**.  In particular, the automated theorem prover is updated to the latest version of WyRL (v0.4.3).  The main improvements are: 1)  the rewrite history is now managed through a single `Automaton` ([#17](https://github.com/Whiley/WhileyRewriteLanguage/issues/17),[#18](https://github.com/Whiley/WhileyRewriteLanguage/issues/18)); 2) an incremental algorithm for implementing efficient `rewrite()` is included, though it is not yet properly incremental ([#19](https://github.com/Whiley/WhileyRewriteLanguage/issues/19),[#28](https://github.com/Whiley/WhileyRewriteLanguage/issues/28)).

   * **Updates to Theorem Prover Rewrite Rules**.  In particular, for the new `requires` clause which is now supported by WyRL ([#548](https://github.com/Whiley/WhileyCompiler/issues/548)).

   * **Improved to Standard Library Specifications**.  Various methods in the standard library (`replace()`, `slice()`, `append()`,`indexOf()`,`lastIndexOf()`) have had their specifications updated to be more complete.  The work to fully specify all parts of the standard library is ongoing, however ([#530](https://github.com/Whiley/WhileyCompiler/issues/530)).

   * **Various misc. bug fixes** ([#536](https://github.com/Whiley/WhileyCompiler/issues/536),[#539](https://github.com/Whiley/WhileyCompiler/issues/539),[#541](https://github.com/Whiley/WhileyCompiler/issues/541),[#550](https://github.com/Whiley/WhileyCompiler/issues/550)).


At this point, the next major improvements I plan to work on are to get type invariants working properly again ([#538](https://github.com/Whiley/WhileyCompiler/issues/538),[#528](https://github.com/Whiley/WhileyCompiler/issues/528),[#469](https://github.com/Whiley/WhileyCompiler/issues/469),[#468](https://github.com/Whiley/WhileyCompiler/issues/468)), and to continue refactoring the compiler ( e.g. [#502](https://github.com/Whiley/WhileyCompiler/issues/502),[#501](https://github.com/Whiley/WhileyCompiler/issues/501),[#474](https://github.com/Whiley/WhileyCompiler/issues/474)).  That should keep me busy enough for a while!  
