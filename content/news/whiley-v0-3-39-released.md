---
date: 2016-03-11
title: "Whiley v0.3.39 Released!"
draft: false
---

Progress has slowed on Whiley now that Trimester 1 and my SWEN221 class with 220+ students has begun!  Despite this, development continues with more contributions from others which is great.  This release is largely a "cleaning up" and "bug fixing" release, rather than landing any big features.
## ChangeList

   * **Parameterised Test cases** ([#580](https://github.com/Whiley/WhileyCompiler/issues/580),[#588](https://github.com/Whiley/WhileyCompiler/issues/588)).  Thanks to @SebastianS90, this simplifies the testing framework.  Previously, each test case corresponded to an entry in a JUnit test file and a source file on disk.  This update employs a useful feature of JUnit allowing us to generate test cases on the fly.  So, the test framework scans the list of available tests in the appropriate directories and generates the list of JUnit test cases from that.

   * **Fail Statement** ([#579](https://github.com/Whiley/WhileyCompiler/issues/579)).  Thanks to @richdougherty, this adds the `fail` statement which is mentioned in the spec and elsewhere.  This should hopefully provide more flexibility when interacting with the verifier.


In addition to this, a number of other bug fixes were made.
## Contributors
Thanks (in no particular order) to the various people who have contributed to this release!

Richard Dougherty ([@richdougherty](https://github.com/richdougherty))
Sebastian Schweizer ([@SebastianS90](https://github.com/SebastianS90))
## In Progress
For the future, I am already working on a revamped `wyil` bytecode format and API.  And, @SebastianS90 is making good progress on an extension to support object lifetimes (as found in Rust).
