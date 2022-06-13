---
date: 2020-07-07
title: "Whiley v0.5.0 Released!"
draft: false
---

And, finally, another release of Whiley is upon us after some two years of waiting! As usual, there are a range of known issues and limitations. But, the main improvements are:
   * **Templates ([RFC#0023](https://github.com/Whiley/RFCs/blob/master/text/0023-templates.md))**.  The introduction of *templates* (a.k.a generics, type polymorphism, etc) is a fairly major improvement for Whiley.  A simple example:
```whiley
function id<T>(T x) -> (T y):
    return x
```
Here, we see the template type `T` is declared as part of the `function` signature.  At this stage, there are no *bounds* or similar, so use cases are fairly limited.

   * **Bidirectional Type Inference ([#996](https://github.com/Whiley/WhileyCompiler/issues/996))**.  The ability to omit explicit template arguments (e.g. `id<int>(1)` above) greatly simplifies code using templates.  Furthermore, the ability to propagate types *forward* through an expression also helps with handling of coercions and native types.

   * **Build System**.  The build system has undergone a fairly significant overhaul (though more is still needed).  One must now specify a `wy.toml` file in order to compile any Whiley code.  This can now include *dependencies* which are then resolved using a local repository, and also using a [remote repository](https://github.com/Whiley/Repository/).  There is a lot of work to do here still.

   * **Quick Check ([#904](https://github.com/Whiley/WhileyCompiler/issues/904)).**  Work on the QuickCheck functionality for Whiley has progressed well, though there is plenty more to do.  This provides a simpler mechanism for checking functions meet their specifications that full-blown verification.  It works by exhaustively enumerating inputs (up to some bounds) for some function to check it meets its specification.  This is based on the [QuickCheck for Haskell](https://en.wikipedia.org/wiki/QuickCheck) system.

   * **For Each ([RFC#0063](https://github.com/Whiley/RFCs/blob/master/text/0063-foreach.md)).** Whiley finally has syntax for a simple for-each loop (e.g. `for x in 1 .. 10:`, etc)

   * **Import With ([RFC#0053](https://github.com/Whiley/RFCs/blob/master/text/0053-imports.md)).** This allows for simplified imports, such as `import std::collections::vector with Vector`.

   * **Strict Subtyping ([RFC#0051](https://github.com/Whiley/RFCs/blob/master/text/0051-subtyping.md))**. This arose from the work on bidirectional type inference, and it remains to be seen how well this works.  In particular, subtyping in Whiley is now more constrained than ever.  For example, we cannot assign a variable of type `int` to a variable of type `nat` without an explicit cast, even if it can be shown that this is safe.

   * **Binary Literals ([#854](https://github.com/Whiley/WhileyCompiler/issues/854)).** This is a simple improvement which enables the use of literals such as `0b001001`, etc.

   * **Reference Lifetimes ([#1014](https://github.com/Whiley/WhileyCompiler/issues/1014))**.  For now, reference lifetimes have been removed.  This was for two reasons.  Firstly, they were interacting badly with templates; secondly, for the currently envisaged `1.0` release of Whiley they are not necessary.


In addition, there have been significant improvements to the JavaScript backend for Whiley, and it is now feasible to write non-trivial web applications.  Some examples can be found here: [Minesweeper](https://github.com/DavePearce/Minesweeper.wy), [Game Of Life](https://github.com/DavePearce/Conway.wy), [WebCalc](https://github.com/DavePearce/WebCalc.wy), etc.
