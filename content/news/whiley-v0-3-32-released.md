---
date: 2015-02-25
title: "Whiley v0.3.32 released!"
draft: false
---

Well, it is with some trepidation that I have released the next version of Whiley. This incorporates a very large number of changes and, unfortunately, should be considered extremely unstable at this time (at least, from the perspective of verification). In particular, the main list of changes includes:
   * **Updated syntax for function and method declarations**.  Thanks to Tim Jones for working through changes to the syntax so that function and method declarations use `->` instead of `=>`. For example, "`function f(int x) -> int`", etc. The goal of this change is just to be more consistent with other programming languages.

   * **Support for nested blocks in WyIL ([#442](https://github.com/Whiley/WhileyCompiler/issues/442))**.  The internal API for managing Whiley bytecodes has been updated to support proper nested blocks.  This is a nice feature and allows a number of previously awkward bugs to be resolved.

   * **Support for true loop invariants ([#455](https://github.com/Whiley/WhileyCompiler/issues/455))**.  The change to support nested blocks also allowed a long await update, whereby true loop invariants are now supported.

   * **Reworked Verification Condition Generator ([#420](https://github.com/Whiley/WhileyCompiler/issues/420))**.  The verification condition generator was completely reworked to support the new nested blocks.  This has enabled some interesting improvements to the way that verification conditions are generated, in particular allowing them to be much more readable than before.

   * **Try/Catch Blocks were removed ([#447](https://github.com/Whiley/WhileyCompiler/issues/447))**.  This simplification was actioned simply to try and reduce the overall complexity of the compiler.  Further such reductions in the syntax of Whiley may follow (e.g. removal of string types).

   * **Back propagation was removed ([#416](https://github.com/Whiley/WhileyCompiler/issues/416))**.  The back propagation transform was previously something of an oddity in the compiler, left over from a previous age.  By making some judicious adjustments to the Java backend, this part of the compiler was eliminated.

   * **Refactored the way that nominal types are handled to retain declared invariants for longer**.  This change means that nominal types are preserved within the compiler for much longer than before.  For example, they now appear in the generated verification conditions, and can be extracted from the WyIL bytecodes, etc.

   * **Flow typing was added to WyCS**.  This is perhaps the most controversial change in the compiler, and one that is currently somewhat broken.  This was necessary to allow the correct handling of constrained union types, which now propagate into WyCS rather than being expanded before.  Although this would probably seem to be a sensible approach, there have turned out to be a large number of unexpected problems.


Anyhow, I would not really recommend downloading and using this version of Whiley!  Sadly, the verification side of things is in a verify broken state.  This is mostly due to the inclusion of flow typing in WyCS.  This was necessary for a few reasons, but I cannot seem to get it to work well.  To be honest, I'm rather disappointed with this release and I need to go back to the drawing board on this one ... :(
