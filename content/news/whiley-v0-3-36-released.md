---
date: 2015-09-10
title: "Whiley v0.3.36 Released!"
draft: false
---

The next version of Whiley is upon us.  Whilst predictably late, this release packs quite a punch and contains a range of changes to the language syntax, and critical updates to the verifier.  Certainly, this version is capable of verifying more programs than any previous version.  The summary of changes includes:
   * **Update list to array syntax ([#515](https://github.com/Whiley/WhileyCompiler/issues/515))**. The syntax for list types has changed from `[int]` to `int[]`, whilst the terminology has changed from "lists" to "arrays".  This brings the synax inline with more familiar languages, and also opens up a few further opportunities.

   * **Remove list append, element of and sublist operators ([#513](https://github.com/Whiley/WhileyCompiler/issues/513))**.  Along with changing from lists to arrays, the set of builtin operators has also been reduced.  This is for several reasons, but primarily as part of the continued move to simplify the language.  This also allowed a large number of open issues related to these operators and e.g. verification to be closed!

   * **Add array generator syntax ([#512](https://github.com/Whiley/WhileyCompiler/issues/512))**. With the removal of list append, a mechanism for creating new arrays of a given size was required.  To facilitate this, syntax was borrowed from Rust for constructing arrays of a given size which are initialised with a given element.

   * **Remove range initialiser syntax ([#505](https://github.com/Whiley/WhileyCompiler/issues/505))**.  The syntax for range initialisers has been removed.  The primary reason for this was to simplify the possible forms for quantifiers and, essentially, to make verification over quantifiers work better.

   * **Big improvements to verifier ([#532](https://github.com/Whiley/WhileyCompiler/issues/532),[#527](https://github.com/Whiley/WhileyCompiler/issues/527)**,**[#526)](https://github.com/Whiley/WhileyCompiler/issues/526)**.  A lot of work has been done on improving the verifier, and a lot of progress has been made.  Still more is in the pipeline, and should follow in subsequent releases.  This has meant that a large number of array programs can now be verified.


In fact, there is a slew of other updates which have been made (see [here](https://github.com/Whiley/WhileyCompiler/issues?q=milestone%3Av0.3.36+is%3Aclosed) for more details).  
