---
date: 2011-08-15
title: "Whiley v0.3.9 Released!"
draft: false
---

So, it's that time again for another update of the Whiley compiler.  Perhaps the most interesting update is that *constraints are back*!  Admitedly, only runtime checking of constraints is back; and, there are quite a few problems with it.  But, it's a step in the right direction, and I'm pretty excited about it.

I've also been doing some more work on the benchmark suite.  In particular, the Java Bytecode disassembler is coming along.  One problem I've encountered, unfortunately, is that my type system implementation remains quite fragile.  I will need to harden this up before the next release, otherwise I'll never get the disassembler working ...
## Performance
Aside from large benchmarks (e.g. Chess and the Disassembler), I've also been adding micro benchmarks (both sequential and concurrent).  For the sequential ones, I've provided a Java implemetation as well for comparison purposes.  I thought it would be interesting to see how Whiley compares, so here we go:

[{{<img class="text-center" src="http://whiley.org/wp-content/uploads/2011/08/raw.jpg">}}](http://whiley.org/wp-content/uploads/2011/08/raw.jpg)

Note the log scale.  As expected, performance is truly woeful.  However, it provides a useful start point for  improving performance ...
## Wyclipse
Another interesting development, is that I've begun the process of  constructing an Eclipse plugin.  Things are pretty rudimentary at the  moment, but I was able to get an editor with syntax highlighting working  quite easily!  You can see the code over on [GitHub](https://github.com/DavePearce/wyclipse).
## ChangeLog

   * Added support for "headless" methods.  A headless method is a method which has side-effects but has no explicit receiver.  Such methods are useful, for example, for implementing constructors.

   * Added ability to iterate strings and dictionaries.

   * Changed semantics for dictionaries to support updating of keys.

   * Put back in support for runtime constraint checking.  The main outstanding issue here is that loop invariants don't work.

   * Turned off constant propagation because it's causing lots of problems in relation to the constraints.
