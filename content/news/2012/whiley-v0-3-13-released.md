---
date: 2012-01-24
title: "Whiley v0.3.13 Released!"
draft: false
---

Well, it's been almost two months in the making, but here's the next release of Whiley.  Quite of lot of changes, although there remain significant issues to resolve --- particularly with the front-end.
## ChangeLog

   * Fixed outstanding problem with list and set types related to type tests.  More specifically, on the negative branch of a type test the correct type was not always being calculated.

   * Added support for open records.

   * Added a CONTRIBUTORS file for recording project contributors.  This is based on the [developers certificate of origin](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/SubmittingPatches) used by the Linux Kernel.

   * Changed syntax for processes to be now "references".  This avoids conflicting the name with OS processes.  So, e.g. type `process T` becomes `ref T`.

   * Changed syntax for dereferncing objects to use `*` and `->`, similar to C.

   * Changed syntax for maps from e.g. `{1->2}` to `{1=>2}`.  This is to avoid conflict with `->` for dereferencing.

   * Changed syntax for processes to syntax for references.  So, e.g. type `process {int x}` becomes `ref {int x}`.  The motivation for this choice is simply to avoid confusion with OS processes.

   * Changed Wyil bytecode to support various "effective" types (e.g. sets, lists, dictionaries).  These enable more efficient operation across a union of similarly kinded types.  For example, we can index into a list of type [int]|[bool] without having to coerce into a list of type `[int|bool]`.

   * Worked hard to get constraints being expanded properly again.  This is working pretty well now for the most part.

   * Added support for Maven compilation (thanks Lee).
