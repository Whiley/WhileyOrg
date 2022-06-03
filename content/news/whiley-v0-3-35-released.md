---
date: 2015-06-19
title: "Whiley v0.3.35 Released!"
draft: false
---

Finally, a release of Whiley that is on schedule!  This includes some fairly significant updates to the syntax of the language itself:
   * **Removal of set and map data types ([#471](https://github.com/Whiley/WhileyCompiler/issues/471))**.  These data types have been entirely removed from both the source language (Whiley), and the bytecode language (WyIL).  This is a pretty radical change, but it relates to my goal of simplifying the language as much as possible to reduce outstanding issues.  In the future, I may consider putting these datatypes back in.

   * **Removal of for loop ([#471](https://github.com/Whiley/WhileyCompiler/issues/471))**.  This follows on from the above change.  Without set and map data types, there is no specific need for a `for` loop.  Therefore, this has removed for now in order that I can focus on getting everything else to work.  In the future, I certainly intend to put some kind of `for` loop back into the language (though it may take a different form).

   * **Tidied up WyRL Examples**.  The Whiley Rewrite Language is a domain-specific language for building declared rewrite systems.  This is used to implement the automated theorem prover in Whiley.  There are a number of examples that come with this, and I have tidied them up so they compile again.


One of the next main objectives will be to split the compiler up into the plugin framework.  This has been on the cards for a while, but it's finally getting traction.  For example, I have begun splitting out the WyRL module into [its own repository](https://github.com/Whiley/WhileyRewriteLanguage) and migrating issues over.
