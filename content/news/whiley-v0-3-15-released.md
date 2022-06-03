---
date: 2012-05-25
title: "Whiley v0.3.15 Released!"
draft: false
---

Finally the next release of Whiley is upon us!  There are a few useful improvements in this release.  In particular, compile-time verification of constraints is again functioning and can be enabled with a switch.
## ChangeLog

   * **Improved performance of the Whiley Build System**.  In particular, this no longer scans all files reachable from the current directory when looking up names in the NameSpace!

   * **Brought back compile-time verification.** This remains very sketchy and your mileage will vary.  However, it's good to have it back!  You can turn compile-time verification on by supplying the following command-line argument: `-X verification:enable=true`

   * **Improved pipeline stage configuration from the command-line**.  All pipeline stages can be configured from the pipeline (e.g. verification above), and the mechanism for doing this has been improved.

   * **Improved the generated WYIL code in some cases**.  The compiler internally generates WYIL files which are then passed through the pipeline.  In some cases, the generated code was unnecessarily poor and that has been tidied up.

   * **Fixed numerous bugs**.  Too many to count, in fact.
