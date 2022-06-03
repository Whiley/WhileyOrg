---
date: 2014-10-09
title: "Whiley v0.3.31 Released!"
draft: false
---

The latest release is upon us, after a short break whilst I was holidaying in Europe!  This includes a few simple bug fixes and updates (see [#433](https://github.com/Whiley/WhileyCompiler/issues/433) and [#392](https://github.com/Whiley/WhileyCompiler/issues/392)), along with one significant feature:
   * **Improved Context Information for Verification Errors ([#435](https://github.com/Whiley/WhileyCompiler/issues/435))**.  When a verification error occurred, it was often difficult to tell which part of a *pre-condition* / *post-condition* was causing it.  Now, context information is included to identify the relevant part of the precondition or postcondition.


As an example to illustrate this context information, consider the following (incorrect) program:

```whiley
function abs(int x) => (int r)
ensures r == x || r == -x
ensures r >= 0:
    //
    return x
```

Compiling this program using the previous version of the compiler (with verification enabled), produced the following error:
```
./test.whiley:5: postcondition not satisfied
    return x
    ^^^^^^^^
``` 

However, this does not tell us which component of the *postcondition* actually failed.  Compiling with the new version gives the following error:
```
./test.whiley:5: postcondition not satisfied
    return x
    ^^^^^^^^

./test.whiley:3: 
ensures r >= 0:
        ^^^^^^
```

Here, we see that the context information consists of additional point(s) in the program which are related.  In this case, it tells us exactly which component of the postcondition is not satisfied.
