---
date: 2012-03-07
title: "Whiley v0.3.14 Released!"
draft: false
---

Finally, it's time for yet another release.  The main change with this release has been a reworking of the compiler framework into a more serious build system called, unsurprisingly, the Whiley Builder System (wybs).  This has helped integration with both Ant and Eclipse.  However, there remain a few aspects of it that need improvement, most notable performance and dependencies.  Nevertheless, I'm very pleased with how the structure of the Whiley compiler is progressing.
## ChangeLog

   * Deployed the new Whiley Build System, which provides a generic framework for managing namespaces and package roots.  This is currently lacking good support for dependency tracking, but it should be easy enough to extend to support this.

   * Fixed quite a few bugs, and have identified quite a few more to be fixed.
