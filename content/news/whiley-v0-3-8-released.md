---
date: 2011-08-01
title: "Whiley v0.3.8 Released!"
draft: false
---

Now that teaching has started up again, development has slowed a little.  This release is primarily a bug fix release.  The benchmarks and examples now all compile again, which is great!  I've also significantly increased the number of micro benchmarks, as I'm gear up for some performance testing ...
## ChangeLog
The main changes since v0.3.7 are:
   * Added proper support for internal message sends.

   * Reworked the JVM implementation behind coercions.

   * Added support for detecting ambiguous coercions, and reporting a syntax error.

   * Added support for an explicit cast operator, which follows C's cast syntax.

   * Fixed numerous bugs

