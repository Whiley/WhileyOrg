---
date: 2013-01-11
title: "Whiley v0.3.18 Released!"
draft: false
---

The next version of Whiley is upon us!  This consists of mostly lightweight improvements over v0.3.17 and various bug fixes (see [issues for more](https://github.com/DavePearce/Whiley/issues?milestone=10&page=1&state=closed)).  I have now been attempting to verify some of the [microbenchmarks in Wybench](https://github.com/DavePearce/wybench), with some useful progress being made (although it is flushing out a lot of issues).
## ChangeLog

   * Lots of improvements to the verifier, both in the generation of verification conditions and the theorem prover itself.

   * Added support for `all { ... | ... }` quantifiers.

   * Fixed some issues related to negated integers appearing in constant definitions.

   * Lots of other miscellaneous bugs fixed.

## Future Work
Work for the next release will focus on improving the verifier and, in particular, getting as many of the micro benchmarks to verify as possible.
