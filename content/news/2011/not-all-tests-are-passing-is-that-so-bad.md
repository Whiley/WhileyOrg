---
date: 2011-11-01
title: "Not all Tests are Passing ... is that so Bad?"
draft: false
---

For the Whiley compiler, I currently have over 500 end-end tests and in excess of 15,000 unit tests (most of which were auto-generated and target the type system).  Each end-end test is a short Whiley program that is  categorised as either *valid* or *invalid*.  Valid tests also include sample output and are expected to compile, execute and produce matching output.  The invalid tests are expected to generate a compile-time error.  To make this more precise, I categorise the kinds of error that the compiler can produce as:* internal failure*, *syntax error* or *verification error*.  Every invalid test is specified to raise either a syntax error or a verification error, and the test will not pass if the compiler does anything else.  Thus, an invalid test which should produce a syntax error will not pass if the compiler barfs out a `NullPointerException`.

Now, the thing is: *not all my end-end tests are currently passing*.  In fact, I don't think it's *ever been the case that all of the tests have passed*.  That may seem like a bad thing, but I think there are some mitigating circumstances:
   * My test suite is constantly growing.  As soon as I spot an error, or think of a possible problem, I add a test.  Adding tests makes me feel good, and I love it!  That's because a test is a piece of knowledge *locked-in*.  Once the test is written and checked in, *I can't forget*.

   * Some failures represent issues that I've given very low priority to.  Eventually, I will get to them ... but not yet.  I do sometimes make use of the `@Ignore` annotation for these kinds of tests.

   * Some failures represent significant design flaws in the system.  They should be high-priority, but represent weeks or months of refactoring and redesigning to fix.  I don't like to `@Ignore` these ones ... I prefer to feel the pain.


In a way, my test suite is like a queue.  My tests never all pass because by the time I fixed all the ones that are failing ... *I've added some more*!

This is similar to [Test-driven development](http://wikipedia.org/wiki/Test-driven_development) I suppose.  What I don't like about TDD though, is that you're supposed to write a test and then immediately make it pass.  That doesn't work for me since,  in a few seconds, I can write a test that might takes months of careful refactoring to solve.   I'm never going to fix those ones immediately ... they need serious [hammock time](http://blip.tv/clojure/hammock-driven-development-4475586)!