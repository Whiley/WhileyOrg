---
date: 2011-04-26
title: "Whiley v0.3.4 Released!"
draft: false
---

Well, after a fairly long haul, the latest version of Whiley is released.  This remains something of a stop-gap for the moment, as there is still quite a lot to do!
## ChangeLog

   * Relicensed the tool to use the ["New BSD License"](http://en.wikipedia.org/wiki/BSD_licenses).  The reason for this is to permit wider distribution of the language.

   * Integrated the new implementation of types in Whiley.  See [this article](http://whiley.org/2011/02/16/minimising-recursive-data-types/) for more on how they work.****

   * Added supported for reference counting of Lists and Sets.  This reduces the amount of cloning required.

   * Added partial support `switch` statements and `exception`s.

   * Changed the way name mangling occurs in class files**. **This now uses a binary format to represent types which is more compact, although somewhat less readable I suppose.

   * Changed the way scoping is determined for local variables.  Previously, `NameResolution` would perform a simplistic dataflow analysis to determine what local variables are "live" at any given point.  These were the local variables, and all others we then assumed to be constants.  To avoid confusion, and because it's hard to deal with complex control-flow at this point, I have made so that if you have an assignment of the form "x = ..." in a function/method then the name "x" corresponds to a local variable *at all points*.

   * Finally renamed the `print` statement to be the `debug` statement.

   * Fixed problem with loading class files when compiling stdlib

   * Fixed an uncountable number of bugs.
