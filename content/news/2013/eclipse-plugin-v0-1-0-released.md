---
date: 2013-11-29
title: "Eclipse Plugin v0.1.0 Released!"
draft: false
---

After being stuck with an outdated Eclipse plugin for quite a while, I've finally released a new version of the Whiley Eclipse Plugin (Wyclipse).  This uses the latest version of the Whiley Compiler (WyC), and fixes a whole host of problems with the previous version.  Specifically:
   * **Whiley Projects are Standalone**.  Previously, every Whiley project was also a Java project, and this caused lots of problems.  Now, when you create a Whiley project, a `.whileypath` file is created to store the project's build path configuration.

   * **Whiley Build Path is Configurable**. You can now configure the Whiley Build Path, by right-clicking on a Whiley project and selecting "Whiley Build Path".  You need to be in the Whiley Perspective for this to show up though.  This gives control over what the compiler considers to be source folder, and where binary files are to be placed.

   * **Verification is Optional.**  Previously, verification was always turned on.  This was a problem because verification is very unstable, and often wouldn't allow a program to compile.  But, now, you can enable or disable it as you wish!  You can even enable it for specific folders, and not others.

   * **Whiley / Java "Dual" Projects.**  You can now actually create a "dual" Whiley and Java project, where some files are written in Whiley and some in Java.  You can then make the Java code call into the Whiley code and vice versa.  Unfortunately, setting this up is not as straightforward as I would like --- mostly because of the way the Java compiler is working.  Still, I'll be trying to make this better in the future.

   * **Whiley Programs can be Run**. It is now technically possible to run Whiley programs from Eclipse.  At the moment, this requires creating a dual project (as above) and calling the Whiley code from a Java wrapper (which you can then launch in the normal way).  Obviously, this is not ideal and I'll be working on this in the future as well.


Right, here are a few screenshots ...

[{{<img class="text-center" src="http://whiley.org/wp-content/uploads/2013/11/Wyclipse1.jpg">}}](http://whiley.org/wp-content/uploads/2013/11/Wyclipse1.jpg)
[{{<img class="text-center" src="http://whiley.org/wp-content/uploads/2013/11/Wyclipse2.jpg">}}](http://whiley.org/wp-content/uploads/2013/11/Wyclipse2.jpg)[{{<img class="text-center" src="http://whiley.org/wp-content/uploads/2013/11/Wyclipse3.jpg">}}](http://whiley.org/wp-content/uploads/2013/11/Wyclipse3.jpg)
Finally, you can install the latest version of the plugin from within Eclipse using the update site: `http://whiley.org/eclipse`
