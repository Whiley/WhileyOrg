---
date: 2014-09-05
title: "Whiley v0.3.30 Released!"
draft: false
---

The next release of Whiley is now ready to be downloaded.  This includes a small number of bug fixes and two more significant changes:
   * [#418](https://github.com/Whiley/WhileyCompiler/issues/418) --- Removal of implicit coercions.  This has some consequences for how you write Whiley programs, and there are probably some follow-on changes needed.

   * [#427](https://github.com/Whiley/WhileyCompiler/issues/427) --- Improved disambiguation of cast expressions versus bracketed expressions.  See[ this blog post](http://whiley.org/2014/09/05/a-story-of-cast-expressions/) I wrote about the problem and its solution.

   * Various other bug fixes (see the [list of closed issues](https://github.com/Whiley/WhileyCompiler/issues?q=milestone%3Av0.3.30+is%3Aclosed) for all)

There are more improvements in the pipeline, particularly related WyIL bytecode format. 
