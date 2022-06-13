---
date: 2013-05-06
title: "Whiley v0.3.19 Released!"
draft: false
---

It is with some disappointment that I've finally decided to release v0.3.19 despite this being almost 3 months overdue!  The disappointment arises because, despite a lot of valiant effort, verification is still not working very well --- and, in fact, is probably worse than the previous release!  However, on the other hand, I have made significant progress in laying some concrete foundations which will underpin the verification process going forward.  Specifically, the main contributions of this release are:
   * **Decoupled Verification**.  Previously, the whole verification process was a mixed up mess of verification condition generation and automata rewriting.  These two components have now been nicely separated through an intermediate language, which we're calling the *Whiley Assertion Language (WYAL)*.  The beauty of this is that `wyal` files provide a nice human-readable interface to the verifier.  For example, we can now look at the verification conditions generated from a `whiley` source file; and, we can modify those conditions and pass them back through the verifier; or, we can write our own assertions from scratch to test the verifier and/or implement some unrelated system.  Furthermore, the verifier itself can be back by different solvers (e.g. Z3, CVC, etc) which might help Whiley get going more quickly.

   * **Updated Whiley Build System**.  I have tweaked the Whiley build system to better support the generation of intermediate files.  In particular, I've introduced "virtual roots" which are the default location for an intermediate file.  Thus, in the default case, an intermediate file is no longer written to disk.  However, by specifying a concrete root (e.g. with a command-line option such as `-wyildir "."`) the corresponding intermediate files are written to disk for debugging purposes and/or general interest.  At the moment, there are three kinds of intermediate file: `wyil`, `wyal` and `wycs` (the latter being the binary expanded format for `wyal` files).


Going forward, my goal is fairly clear: *improve the verifier to pass more tests*.  For those who are interested, I have written up [a few thoughts on what's wrong](https://github.com/DavePearce/Whiley/issues/262).
