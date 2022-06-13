---
date: 2014-08-14
title: "Whiley v0.3.27 Released!"
draft: false
---

The next release of Whiley is upon us.  This includes a large number of bug fixes, and a significant rewrite of the verifier.  Unfortunately, the verifier is not yet verifying many more examples, but it's now placed to do so.  Specifically, the main highlights are:
   * **Better Support for Contractive Types**.  Contractive types are those which cannot accept any value constructable within the language itself.  In essence, they are equivalent to `void`.  An example would be something like `type Rec is { Rec x }`.  This type is contractive because is only describes values of infinite height.

   * **Reworked Automaton Rewriter**.  The IterativeRewriter is responsible for rewriting automatons, which goes to the heart of how the verifier works.  This component has been significantly reworked to eliminate numerous bugs.  Unfortunately, this has meant that performance is somewhat worse, and this will need to be addressed in the future.

   * **Quantifier Instantiation**.  The verifier is now capable of performing much more advanced forms of quantifier instantiation.  More needs to be done here, however, but the basic framework is now in place.  See [#399](https://github.com/Whiley/WhileyCompiler/issues/399) and [#379](https://github.com/Whiley/WhileyCompiler/issues/379).
