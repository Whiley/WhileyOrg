---
date: 2018-04-11
title: "Whiley v0.4.2. Released!"
draft: false
---

And, after a long while, another official release of Whiley is here.  This is something of an interim release whilst other things are brewing in the background.  There also some known issues with this release.  The main changes are:
   * **Fully Qualified Names**.  The syntax of fully qualified names has changed.  Specifically, `::`  is used in place of `.`  for separating package names.  For example, a name such as `std.array`  is now `std::array`  (see [RFC#13](https://github.com/Whiley/RFCs/blob/master/text/0013-qualified-names.md)).

   * **Removal of negation and `any`  types**  ([RFC#20](https://github.com/Whiley/RFCs/blob/master/text/0020-anyneg.md)). This also includes the temporary removal of intersection types ([#843](https://github.com/Whiley/WhileyCompiler/issues/843)) and the replacement of (internal) negations with difference types ([#827](https://github.com/Whiley/WhileyCompiler/issues/827)).  The latter improves error messages.  For example, an error such as `expected type int, found type (int|null)&!int`  becomes `expected type int, found type (int|null)-int` .  This is all part of my push towards a proper "low level" API for building backends (see [RFC#21](https://github.com/Whiley/RFCs/blob/master/text/0021-wyll.md)).

   * **Support `final`  modifier**.  Support has been added for a `final`  modifier, similar to that found in Java (see [RFC#5](https://github.com/Whiley/RFCs/blob/master/text/0005-final-modifier.md)).  In particular, this required the addition of a new compiler phase for checking [definite unassignment](https://en.wikipedia.org/wiki/Definite_assignment_analysis).

   * **Empty Array Initialisers**.  Finally, the empty array initialiser `[]`  is back!  For various reasons this had presented some challenges for type checking, and was particularly frustrating as it caused problems with empty string initialisers `""`  as well (see [#692](https://github.com/Whiley/WhileyCompiler/issues/692)).

   * **Improved Verification**.  In addition, there have been many improvements to the theorem prover and verification in general, though lots remains to be done here (see e.g. [#143](https://github.com/Whiley/WhileyTheoremProver/issues/143), [#141](https://github.com/Whiley/WhileyTheoremProver/issues/141), [#140](https://github.com/Whiley/WhileyTheoremProver/issues/140), [#138](https://github.com/Whiley/WhileyTheoremProver/issues/138), [#137](https://github.com/Whiley/WhileyTheoremProver/issues/137), [#136](https://github.com/Whiley/WhileyTheoremProver/issues/136), [#131](https://github.com/Whiley/WhileyTheoremProver/issues/131), [#128](https://github.com/Whiley/WhileyTheoremProver/issues/128), [#124](https://github.com/Whiley/WhileyTheoremProver/issues/124)).


At the moment, I am continuing to make progress towards a realistic low-level API which will allow for a greater range of backends (e.g. C/LLVM).
### Known Issues
There is one known issue with this release:
   * The JVM backend is currently offline.  Specifically the command `wy jvmcompile ...`  will not succeed.  This is related to ongoing work towards a low-level API and we should expect it to come back online ASAP.
