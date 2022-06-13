---
date: 2016-01-29
title: "Whiley v0.3.38 Released!"
draft: false
---
Finally, just over one month since the last release of Whiley, version v0.3.38 is released today! The list of changes is reasonably large and we should expect lots more going forward ...

## ChangeList   

   * **Removed Tuple Types** ([#537](http://github.com/Whiley/WhileyCompiler/issues/537)).  Part of my ongoing work to simplify the language.  Tuple types were not heavily used in any of my benchmarks and are not really needed because records fulfill a similar purpose.

   * **Updated Syntax for Return Types** ([#463](http://github.com/Whiley/WhileyCompiler/issues/463)).  The primary situation where tuple types were useful was that they supported multiple return values.  Therefore, the syntax for `function` and `method` return types has been updated to support multiple returns.  This also meant the rather awkward `TypePattern` was eliminated (finally).

   * **Removed `real` Type** ([#495](http://github.com/Whiley/WhileyCompiler/issues/495)).  This is part of my ongoing work to simplify the language.  Whilst this seems pretty drastic, the fact remains that the `real` datatype was hardly used and is not critical at this stage to the project.  Furthermore, there were numerous open issues against it.

   * **Support for `continue` statement** ([#327](http://github.com/Whiley/WhileyCompiler/issues/327)).  Thanks to [@richdougherty](https://github.com/richdougherty) for finally resolving this issue which has been open since early 2014!

   * **Travis CI now compiles and tests code** ([#497](http://github.com/Whiley/WhileyCompiler/issues/497)).  Thanks also to [@richdougherty](https://github.com/richdougherty) for finally adding Ant support for running all JUnit tests.  The main benefit is that Travis CI now compiles and tests code, whereas before it was just compiling it.

   * **Simplified WyIL Bytecode Representation** ([#574](http://github.com/Whiley/WhileyCompiler/issues/574)).  In addition to simplifying the language, I am also beginning now to go through refactoring the compiler.  This aims to improve overall quality and reduce the amount of code we have.

   * **Improved README with instructions on building compiler in Eclipse** ([#558](http://github.com/Whiley/WhileyCompiler/issues/558)).  This should make it easier for people to contribute to the compiler.

   * **Various Bug fixes** ([#551](http://github.com/Whiley/WhileyCompiler/issues/537),[#552](http://github.com/Whiley/WhileyCompiler/issues/552),[#554](http://github.com/Whiley/WhileyCompiler/issues/554),[#567](http://github.com/Whiley/WhileyCompiler/issues/567), [#577](http://github.com/Whiley/WhileyCompiler/issues/577)).  Thanks to [@utting](https://github.com/utting), [@DrewStatford](https://github.com/DrewStratford) and [@SebastianS90](https://github.com/SebastianS90) for spotting and fixing various bugs.

## Contributors:
Thanks (in no particular order) to the various people who have contributed towards this release!
Richard Dougherty ([@richdougherty](https://github.com/richdougherty))
 Mark Utting ([@utting)](https://github.com/utting)
 Drew Stratford ([@DrewStatford](https://github.com/DrewStratford))
 Sebastian Schweizer ([@SebastianS90](https://github.com/SebastianS90))

