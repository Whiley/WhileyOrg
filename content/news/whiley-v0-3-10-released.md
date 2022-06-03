---
date: 2011-09-21
title: "Whiley v0.3.10 Released!"
draft: false
---

Well, it's been a tough slog.  But, finally, we have a new release of Whiley!!  The main thing that's improved over the past few weeks is the underlying type implementation.  This was causing problems before, as programs which should type-check were failing and vice-versa.  To resolve this, the type system has been reimplemented from scratch and (hopefully) it should be significantly better.  In particular, I've done quite a lot more testing (e.g. I now have around 15,000 individual unit tests for the `Type` class).

The other main difference is the way in which `import` statements are handled.  Whilst this is definitely a step in the right direction, it's not without some outstanding issues --- which I discussed in more detail [here](http://whiley.org/2011/09/03/namespaces-in-whiley/).
## ChangeLog

   * Changed the way imports are interpreted.  Previously, `import whiley.lang.String` would have imported all symbols from module `String`.  Now, it only imports the module name.  So, for example, to access the method `indexOf`, you need to write `String.indexOf(s,i)`.  However, you can still replicate the old approach by directly importing the names from a module.  For example, `import * from whiley.lang.String` imports all names from the `String` module

   * The entry point `main()` no longer has `System` as its receiver.  Instead, `System` is a parameter and `main` is a headless method.  This is necessary as, otherwise, the `System` process is blocked until main completes!

   * Split out the type system into a separate library called wyautl.  As part of this, I've essentially reimplemented the type system from scratch in an effort to really harden it up.  I've done a significant amount of testing, and it's definitely a lot better.  The type system now directly supports *negation* and *intersection* types, which makes for some interesting possibilities.

   * Support for dictionaries is somewhat improved.  In particular, you can now create an empty dictionary!  An empty dictionary is denoted `{->}` (contrasting with `{}` for sets and `[]` for lists).

   * Support for try-catch blocks has been added (finally).  This means you can now catch exceptions in Whiley.  At the moment, however, the system does not check that you properly declare your exceptions ... but that will come shortly.

   * Improved the JavaDoc documentation for the compiler.  I plan to make this documentation visible soon, in conjunction with detailed discussion of how the compiler actually works.

   * Various bug fixes.
