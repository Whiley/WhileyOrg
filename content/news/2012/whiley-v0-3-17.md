---
date: 2012-12-07
title: "Whiley v0.3.17 Released!"
draft: false
---

Whilst it's been over *three months* since the last release of Whiley, this latest release is chocked full of improvements!  I've closed [around 60 issues](https://github.com/DavePearce/Whiley/issues?milestone=9) in that time, and have completely reworked the theorem prover from scratch.  This means compile-time checking of constraints is starting to work better --- however, there remains quite a way to go.  This release also includes an experimental back-end [being developed by Art Protin](https://github.com/protin2art) for translating Whiley programs into C code so they can be compiled to machine code.
## ChangeLog   

   * **Theorem prover rebuilt from scratch**.  The automated theorem prover which is used to check [verification conditions generated during compilation](http://) is automatically generated from a domain-specific rewrite language.  Currently, this DSL is packaged into the Wyone module (although I may rename this to WYRL in the future for obvious reasons).  The generated theorem prover is [over 74KLoc of Java code in a single file](https://github.com/DavePearce/Whiley/blob/devel/modules/wyil/src/wycs/Solver.java)!  Yes, you heard right.  I think, as I improve the code generation process, this will come down (hopefully dramatically, though we'll see).

   * **Backend for generating C**.  An experimental backend for translating Whiley programs into C programs has been [developed by Art Protin
](https://github.com/protin2art) over the last few months, and is showing promise.  Note, however, that this remains extremely experimental!

   * **Added Support for Ad-Hoc Indentation**.  Previously, I strictly required 4 spaces for indentation.  However, I noticed that this really caused a lot of problems when people were using different text editors.  Following the lead from [Coffeescript](http://coffeescript.org/), I've modified the parser to accept *ad-hoc indentation*.  Basically, at the start of a block you need to indent at least one space.  The first indentation then sets the indentation level for the rest of the block.

   * **Constant propagation re-enabled**.  The constant propagation phase in the compiler helps improve the quality of generated code in a number of ways.  For some time now, it has been disabled for various reasons and, finally, I got around to fixing it.

   * **Deadcode elimination improved**.  The elimination of deadcode has been improved which, in turn, has dramatically improved the quality of the generated Wyil files.

   * **Numerous Bugs fixed**.  Literally, hundreds of them.

## Future Work
For the next release of Whiley, I've already got [26 open issues](https://github.com/DavePearce/Whiley/issues?milestone=10&state=open).  My focus is still on improving the automated theorem prover to the point where I can have compile-time verification enabled by default.  However, there are some important areas which have been neglected for some time, including: the standard library; syntax for objects; simple parsing problems; and the eclipse plugin.  I really need to put some time into these as well, in order to get something which is genuinely useable by others...
