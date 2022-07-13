---
date: 2013-12-19
title: "Proposed Syntax Changes for Whiley"
draft: false
---

Now that I've had the chance to write [a reasonable amount of code in Whiley](https://github.com/Whiley/WyBench/), it is time to reflect on some things I don't like.  In particular, there are a number of issues with the syntax which I'd like to improve which I'll document here.

## Function & Method Declarations

Currently, the syntax for a function or method in Whiley looks something like this:
```whiley
int abs(int x) 
// Return value cannot be negative
ensures $ >= 0:
    //
    if x >= 0:
       return x
    else:
       return -x
```
Although I quite like this syntax, I very much dislike the use of `$` for indicating the return value in a post-condition (i.e. `ensures` clause).  It occurred to me that explicit naming of the return value would be better (in fact, [Dafny](https://dafny.org) does this already).  So, my proposed new syntax for function declarations is thus:
```whiley
function abs(int x) => (int y)
// Return value cannot be negative
ensures y >= 0:
    //
    if x >= 0:
       return x
    else:
       return -x
```

Strictly speaking, the `function` keyword is not necessary, however I think it adds some clarity.  In particular, *functions* (which are {{<wikip page="Pure_function">}}pure{{</wikip>}}) now contrast explicitly with *methods* (which may have side-effects):
```whiley
method read(String filename) => ([byte] y)
    //
    f = File.Reader(filename)
    ...
```
Note, the syntax for `method` declarations is still not finalised, and I've been discussing it at length over in the issue tracker (see {{<issue id="204">}}, {{<issue id="309">}} and {{<issue id="310">}}).

The final aspect of the proposed syntax change is that *you can omit the return value when it's `void`*.  For example, this:
```whiley
void ::f(Reader r):
   ...
```
becomes this:
```whiley
method f(Reader r):
   ...
```
Although this is hardly a significant issue, is still a nice abbreviation.

## Type and Constant Declarations
One of things I really like about the current syntax for Whiley is the use of the `define` statement, which is simple and clean.  However, it turns out there were some issues I hadn't considered.  The issue revolves around the fact that the `define` keyword is overloaded.  For example:
```whiley
define PI as 3.1415926536      // defines a constant
define nat as int where $ >= 0 // defines a type!

nat f():
    return Math.round(PI)
```
Here, we see `define` being used for defining a new constant, as well as a new type.  This is problematic, since the compiler must figure out which it is.  Of course, it can do that but, unfortunately, this leads to difficult to understand error messages.  The compiler initially assumes a `define` statement defines a type and, if this fails, backtracks and assumes it defines a constant.  For example:
```whiley
define Point as {int x, int y,}
```
This produces the following cryptic error message:
```
./test.whiley:1: unrecognised term (int)
define Point as {int x, int y,}
                 ^^^
```

The programmer was trying to define a new `Point` type, but accidentally left a comma at the end.  The error message is confusing, because it appears to say the `int` type doesn't exist!  Ultimately, the problem is that the compiler initially tried to parse it as a type, but failed.  So, it backtracked and tried for a constant which also failed, this time leaving an error message about why `{int x, int y,}` is not a well-formed expression.

The proposed syntax for constants and type declarations tries to be consistent with that for functions and methods:
```whiley
constant PI is 3.1415926536      // defines a constant
type nat is (int x) where x >= 0 // defines a type!
```
With this syntax, there is no ambiguity between what is supposed to be a constant and what is supposed to be a type.  Furthermore, I've removed the `$` syntax in favour of explicitly named variables.

## Local Variable Declarations
One of the unusual aspects of the current syntax is that you cannot *declare* local variables.  Whilst this is nice, it does causes problems.  One of these arises in verification, and wasn't something I initially considered.  For example:
```whiley
define nat as int where $ >= 0

nat sum([nat] xs):
   r = 0 // result
   i = 0 // index
   while i &lt; |xs| where i >= 0 && r >= 0:
      r = r + xs[i]
      i = i + 1
   //
   return r
```
This is a simple example illustrating that summing over a list of natural numbers yields a natural number.  The loop invariants are, alas, necessary for the verifier to accept this program.  In principle, the compiler could attempt to infer these loop invariants since they are simple.  

Another option (which I prefer) is to allow variable declarations:
```whiley
nat sum([nat] xs):
   nat r = 0 // result
   nat i = 0 // index
   while i &lt; |xs|:
      ...
```
Since `r` and `i` are both declared to be of type `nat`, the loop invariants are no longer required since the verifier will enforce the `nat` constraints at all program points.

There are still some unresolved questions here.  Firstly, I will probably still allow variables to be declared as `var`, which means they can take any type at any point.  Furthermore, flow typing will still be used to restrict the type of a variable in various ways.  For example:

```whiley
int get(int|null x):
    if x is int:
        return x // automatically retyped
    else:
        return 0
```

And, similarly:

```whiley
int f():
    int|null x = null
    ... // here, x has type null
    x = 1
    ... // now, x has type int
    return x
```

Finally, an interesting question is whether or not there is any difference between the declaration `any x` and `var x`.  I'll have to think about this!

## References

Currently, reference types are denoted with the `ref`, like so:
```whiley
define Point as {int x, int y}

void ::shift(ref Point p, int amount):
    p->x = p->x + amount
```
Here, method `m` accepts a *reference* to a `Point` object.  Therefore, by assigning through it, we can produce a side-effect.  My proposed syntax change is [inspired by the syntax for borrowed pointers in Rust](http://static.rust-lang.org/doc/0.4/rust.html#type-system):

```whiley
type Point is {int x, int y}

method shift(&Point p, int amount):
    p->x = p->x + amount
```

For some reason, I prefer `&` over e.g. `*` (as in C).  Also, it remains an open question as to whether or not to stick with the C-like notation of `->` for dereferencing fields and, likewise, `*` for general dereferencing.

Thoughts and comments welcome!!
