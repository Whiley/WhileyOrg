---
date: 2014-09-01
title: "Whiley v0.3.29 Released!"
draft: false
---

The next release of Whiley is now ready to be downloaded.  This includes a number of bug fixes, along with a change in the WyIL bytecode format.  The latter is ahead of further planned changes to improve the bytecode format and verification.  The list of changes is:
   * [#423](https://github.com/Whiley/WhileyCompiler/issues/423) --- Bug fix related to parsing `wycs` files.

   * [#421](https://github.com/Whiley/WhileyCompiler/issues/421) --- Added compiler switch to select external SMT solver (e.g. Z3) for use with verification.  This employs the SMT translator developed by [Henry Wylde](https://github.com/hjwylde).

   * [#419](https://github.com/Whiley/WhileyCompiler/issues/419) --- Improved error reporting for unexpected end-of-file errors during parsing

   * Various other bug fixes (see the [list of closed issues](https://github.com/Whiley/WhileyCompiler/issues?q=milestone%3Av0.3.29+is%3Aclosed) for all)


There are more improvements in the pipeline, particularly related to implicit coercions (see [#418](https://github.com/Whiley/WhileyCompiler/issues/418)). 
