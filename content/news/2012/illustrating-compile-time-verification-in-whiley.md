---
date: 2012-05-28
title: "Illustrating Compile-Time Verification in Whiley"
draft: false
---

With the [latest release of Whiley](http://whiley.org/2012/05/25/whiley-v0-3-15-released/), compile-time checking of constraints can be enabled with a command-line switch.  So, I thought a few examples of this were in order.
## Example: Absolute of an Integer
Consider this simple program:

```whiley
type nat is (int x) where x >= 0

function abs(int x) -> nat:
    return x
```

This defines a type `nat` which is an `int` whose values are non-negative.  The function abs`(int)` accepts an `int` and returns a `nat`.  However, it contains a bug because `int` does not subtype `nat` (since `int` includes negatives whilst `nat` does not).  We can compile this on the command-line like so:

```% wyjc -X verification:enable=true example.whiley
./example.whiley:4: constraint not satisfied
    return x
    ^^^^^^^^
```

The command-line switch `-X verification:enable=true` turns on compile-time verification.  This is not enabled by default because it is experimental.  As we can see, the compiler has correctly spotted the error on line 4.  We can fix the code like so:

```whiley
type nat is (int x) where x >= 0

function abs(int x) -> nat:
    if x >= 0
        return x
    else:
        return -x
```

This will now compile correctly with verification enabled.  As you can see the verifier is able to correctly reason about the effect of conditional statements.

## Example: Maximum of two Integers
As another illustration, consider the following (broken) implementation of the `max(int,int)` function:

```whiley
function max(int x, int y) -> int:
    if x < y:
        return x
    else:
        return y
```

At this point, the function does the *opposite* of what you would expect (i.e. it computes the minimum of `x` and `y` because of a bug).  However, the function will compile with verification enabled because the code meets the given specification.  Let us improve the specification a little by introducing some constraints:

```whiley
function max(int x, int y) -> (int r)
ensures r == x || r == y:
    if x < y:
        return x
    else:
        return y
```

The given constraint states the return value `r` is equal to either `x` or `y`.  However, this constraint is not strong enough to enforce that the maximum of `x` and `y` is returned.  Hence, the code still compiles even with verification enabled.  Finally, we add the missing bit:

```whiley
function max(int x, int y) -> (int r)
ensures (r == x || r == y) && x <= r && y <= r:
    if x < y:
        return x
    else:
        return y
```

Compiling the above with verification enabled now gives the following error:

```% bin/wyjc -X verification:enable=true max.whiley
./max.whiley:3: postcondition not satisfied
        return x
        ^^^^^^^^
```

At this point, we can fix the bug by changing the condition to be `if x > y` and it will compile correctly with verification enabled.

