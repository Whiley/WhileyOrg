---
date: 2013-08-16
title: "Whiley v0.3.20 Released!"
draft: false
---

Well, this release is about 2 months overdue, but it embodies a lot of work. The main changes are:
   * **Bug fixes**. I've closed [around 36 issues](https://github.com/DavePearce/Whiley/issues?milestone=11&page=1&state=closed), many of which were intricate little bugs.

   * **Improved the verifier.** Perhaps what has taken most time is the considerable amount of work I've into improving the verifier.  This is still ongoing, but certainly things are in a much better shape than before.  This has included completely reworking and documenting the rewrite rules of the verifier itself; also, completely reworking the `WyRL` rewrite system to: 1) generate more efficient code; 2) enable different heuristics for applying rewrites; 3) to perform some complexity analysis on rewrite rules to identify which should be prioritised.  Supporting this, I've written a number of simple initial heuristics, and there is currently one clear winner.  However, a lot more work is needed on this.


Going forward, my objective as before: *improve the verifier to pass more tests*.
