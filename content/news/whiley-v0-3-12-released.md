---
date: 2011-12-02
title: "Whiley v0.3.12 Released!"
draft: false
---

Well, crikey, what a long time since the last release.  Things haven't changed a whole lot, apart from various bug fixes.  Probably the most interesting update is the inclusion of *reference counting* of compound structures to enable in-place updates and prevent unnecessary cloning.  This leads to some nice performance improvements.  Quite a bit of work has been done on the benchmarks as well, and also the eclipse plugin.
## ChangeLog

   * Added support for proper reference counting of compound structures.  This employs a live variables analysis to determine when a local variable is dead.

   * Reworked the name resolution and module loading system.  This was done primarily to support build tools such as ant and eclipse.

   * Improved the Ant task.

   * Further improved the runtime checking of constraints.

   * Added some rudimentary reporting of memory usage by the various compiler stages.
