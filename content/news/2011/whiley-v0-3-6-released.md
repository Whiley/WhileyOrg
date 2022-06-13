---
date: 2011-06-26
title: "Whiley v0.3.6 Released!"
draft: false
---

After an untold number of commits, bug fixes and passing unit tests, the next version of Whiley is released!!  I am trying to lock down the syntax of the language as much as possible now, although there are still a number of open issues.

Finally, whilst I'd love to say "go and use this version" ... frankly, you probably shouldn't!  There remain quite a few problems, and the benchmark suite doesn't even compile.  The switch to using the new bytecode-oriented intermediate language (wyil) was very significant, and it'll take a little while to settle down.  Hopefully, the next release will be much sooner ...

## ChangeLog

   * Changed the Whiley Intermediate Language (Wyil) to be a proper bytecode format.  This simplifies many things, and enables easy implementations of interpreters and virtual machines.

   * Changed syntax for synchronous and asynchronous message sends from `<->` and `<-` to `.` and `!`

   * Changed syntax for top type from `*` to `any`

   * Changed syntax for type tests from `~=` to `is`

   * Added a first-class `string` type.  Currently, there is no `char` type --- this may or may not get added eventually.  The reason for adding this type is to allow for better conversions from data types to strings.  In particular, I want strings to displayed as strings, rather than just lists of integers.

   * Changed the underlying model of types from the "ideals" to the "reals".  See [this blog post](http://whiley.org/2011/06/20/on-the-duality-of-types-the-ideals-versus-the-reals/) for more.  As part of this, `int` values are now implemented as `BigIntegers` with real types being implemented as `BigRationals`.

   * Implemented a simpler, but more complete mechanism for performing type tests.  This is probably slightly less efficient than before, because much of it takes place in the runtime library code rather than being hard-coded into JVM bytecode.

   * Implemented a simpler approach to performing type coercions, which is based on the mechanism for type tests.  However, I'm not convinced it's actually making things better.

   * Put in place the basic mechanism for implementing reference counting of compound data structures.  At this stage, I don't actually use reference counting ... but that will come soon enough!

## To Do Next

   * Sort out the implicit coercions

   * Implement complete code for coercions

   * Add proper first-class tuples to wyil

   * Fix up problems with function refs, and add support for method refs (and possibly `interfaces`)

   * Add support for iterating dictionaries (kind of important)

   * Fix the `multistore` bytecode so it's a little less chaotic.

   * Fix problems with `fieldload`, `listload`, `dictload` and effective "union" types

   * Adjust wyil so strong correlation between bytecodes and program statements (probably requires explicit logical not, and, or and xor operators)

   * Adjust wyil to support "named" types to make it a little more human readable (and hopefully to help with error messages as well).

   * Fix up exceptions: 1) to check for the required throws clause; 2) to support try-catch blocks.
