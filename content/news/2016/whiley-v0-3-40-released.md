---
date: 2016-05-28
title: "Whiley v0.3.40 Released!"
draft: false
---

The next version of Whiley is upon us, and this one includes a bumper package of changes.  In particular, I am very excited by the introduction of *reference lifetimes* into Whiley.

## ChangeList

   * **Reference Lifetimes** ([#642](https://github.com/Whiley/WhileyCompiler/pull/642)).  This represents a fairly significant step forward in the evolution of the Whiley language.  Reference lifetimes have been implemented by Sebastian Schweizer, and are heavily influenced by [lifetimes in Rust](https://doc.rust-lang.org/book/lifetimes.html).  Lifetimes in Whiley are similar to those in Rust, but are not currently coupled with any form of "ownership" or "borrowing".  These things may be added late in some form, but not yet.  Lifetimes are important because they provide a pragmatic solution to the problem for deallocation of heap-allocated memory without the need for a garbage collector.

   * **Bug fixes** (e.g. [#602](https://github.com/Whiley/WhileyCompiler/pull/602),[#604](https://github.com/Whiley/WhileyCompiler/pull/604),[#613](https://github.com/Whiley/WhileyCompiler/pull/613),[#625](https://github.com/Whiley/WhileyCompiler/pull/625),[#631](https://github.com/Whiley/WhileyCompiler/pull/631),[#632](https://github.com/Whiley/WhileyCompiler/pull/632),[#634](https://github.com/Whiley/WhileyCompiler/pull/634),[#636](https://github.com/Whiley/WhileyCompiler/pull/636),[#639](https://github.com/Whiley/WhileyCompiler/pull/639)). There were also quite a few small bug fixes made to the code base by various contributors.

## Contributors
Thanks (in no particular order) to the various people who have contributed to this release!

Richard Dougherty ([@richdougherty](https://github.com/richdougherty))
Sebastian Schweizer ([@SebastianS90](https://github.com/SebastianS90))
## In Progress
This will be the last release in the `0.3.X` release series, which has been ongoing since [November 2010](/2010/11/03/whiley-v0.3.1-released/).  The intention is that future major releases will occur in a shorter time frame!

The main change scheduled for the next release will be a complete redesign of the WyIL bytecode language (see [#620](https://github.com/Whiley/WhileyCompiler/pull/620)).  I've already been working on this for some time, and things are coming together.  The key changes are that WyIL will no longer be an *unstructured* intermediate language, and will no longer be *flow typed*.  Instead, it will be something closer to an Abstract Syntax Tree, but with explicit coercions to handle flow typing at the source-level.  The reason for this is to simplify the Verification Condition Generator, which has been extremely troublesome to maintain due to the need to work with unstructured and flow typed control flow.  Furthermore, implementing code generators on the back-end is made significantly harder by the presence of flow typing.

In pitching WyIL at a higher level, the intention is later to introduce a "low-level" intermediate language, WyLL.  This will be unstructured and closer to something which can more easily be turned into machine language, etc.
