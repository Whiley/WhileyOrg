---
date: 2011-07-07
title: "Whiley v0.3.7 Released!"
draft: false
---

Development has continued at a fairly quick pace since the last release of Whiley.  However, with the impending start of term, things are bound to slow down.  Therefore, I'm making a release now a little sooner that otherwise planned.  This fixes a number of important bugs, finally allowing the compiler to compile my benchmark suite again.
## Issues

   * The syntax for synchronous and asynchronous message sends is still causing headaches.  I've summarised the main problems [in this post](http://whiley.org/2011/06/28/disambiguating-ambiguous-syntax/).

   * I'm also a little concerned about my rules for implicit coercions.  For example, for a set union operation with type `{real}+[int]`, the right-hand side is implicitly coerced to be `{int}` and, hence, the result type is `{real|int}`.  In contrast, things behave slightly differently for an intersection with type `{real}&[int]`.  In this case, the right-hand side is coerced into `{real}`, not `{int}`.  The reason for this is that, otherwise, the operation doesn't make sense --- as `{real}&{int}` would always return the empty set.  These rules seem a little confusing to me, and I suspect I need a clearer (perhaps less powerful) model.

   * I'm a little uneasy over the list append and set union regarding element additions.  For example, in an append of type `[int]+int`, the right-hand side is added as an element type of `[int]`.  I'm just not sure if I like this or not.

## ChangeLog

   * Added first-class `char` and `byte` types, which compile down to their primitive equivalents on the JVM.  A `byte` is somewhat different from that in Java, however, as it is *not interpreted*.  That is, it corresponds simply to a sequence of 8 bits.  You can perform the usual array of bitwise operations (`&`, `|`, `^`, `<<` and `>>`).  However, unlike Java, a `byte` will not implicitly coerce into an `int`. Instead, you have to use a method which constructs an `int` assuming some kind of bit representation.  Probably the most common one will be `le2uint(byte)`, which generates and unsigned integer from a byte assuming a [little endian](http://wikipedia.org/wiki/Endianness) layout.  More discussion of the `byte` type can be [found in this post](http://whiley.org/2011/07/04/bits-bytes-more-ambiguous-syntax/).

   * Added support for method pointers.  This allows references to methods to be passed around, just like for function pointers.  An example method pointer type would be `int(Reader)::(int)` --- this indicates a pointer to a method whose receiver is a `Reader` and which accepts an `int` parameter and returns an `int` value.

   * Fixed a lot of bugs.
