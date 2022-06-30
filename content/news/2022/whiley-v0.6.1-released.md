---
date: 2022-06-27
title: "Whiley v0.6.1 Released!"
draft: false
---

Finally, after almost a year since the last release, we have two new releases of Whiley! `v0.6.0` was released on [June 1st 2022](https://crates.io/crates/whiley/versions), and was quickly followed by `v0.6.1` which included an important bug fix.  The main difference is that Whiley is now partly written in Rust and deployed using `cargo` (see [install](/install) for details).  

## Change Log

A summary of the main changes since `v0.5.3`:

* **Improved Verification**.  Verification in Whiley continues to get stronger with further improvements to the Boogie backend (see [this post](https://whileydave.com/2022/05/31/whiley-gets-rusty/) and [our paper](https://whileydave.com/publications/pug22_jar/) for more info).  The Boogie backend is now the default verification toolchain and passes >95% of tests.

* **Command-Line Tool** ([Repo](https://github.com/Whiley/WhileyBuildTool)).  The command-line tool `wy` for building and verifying Whiley programs is now [written in Rust](https://whileydave.com/2022/05/31/whiley-gets-rusty/).  In essence, this provides a wrapper around the existing Java components (see [this post](https://whileydave.com/2022/05/31/whiley-gets-rusty/) for more).  This also adds support for the commands `clean` ({{<issue id="1092">}}) and `init` ({{<issue id="26" repo="WhileyBuildTool">}}), amongst other things.

* **Old Syntax** ({{<issue id="1096">}}).  The ability to reason about heap structures has improved dramatically and, in particular, now supports `old()` syntax (following [JML](http://www.jmlspecs.org/index.shtml), [Dafny](https://github.com/dafny-lang/dafny) and similar systems).  This gives the ability to reason about the state of the heap prior to a method:
   ```whiley
   method inc(&int x)
   ensures old(*x) < *x:
     *x = *x + 1
   ```

   Here, `old(*x) < *x` effective says that the value at `*x` must
   increase after calling this method.  See {{<rfc id="67"
   name="0067-old-values">}} for further discussion

* **Property Syntax** ({{<issue id="1102">}}, {{<issue id="1151">}}, {{<issue id="1157">}}).  The syntax for properties has become more expressive with the ability to specify the return value, and use `if` statements and variable declarations within the body:

   ```whiley
   property sum(int[] xs, int i) -> (int r):
     if i < 0 || i >= |xs|:
       return 0
     else:
       return xs[i] + sum(xs,i+1)
   ```
   See {{<rfc id="102" name="0102-property-syntax">}} for further discussion (though note the implement syntax differs somewhat).

* **Exponentiation Operator** ({{<issue id="1124">}}).  Support has been added for the exponentiation operator `x ** y` which returns `x` to the power of `y`.  Thus, for example, `2 ** 4` returns `16`.  A precondition of this operator is that `y` cannot be negative.

* **Test File Format** ({{<issue id="978">}}, {{<issue id="1149">}}).
  A new test file format has been developed for improved testing of
  the compiler.  This now allows a single test to describe multiple
  files and offers a dynamic view of files.  That is, a single test
  can test a file followed by _changes to that file_.  The following
  illustrates such a test:
  ```
  ====
  >>> main.whiley
  function f(int x, int y) -> int:
    return x ** y

  public export method test():
    assume f(2,-1) == 2
  ---
  E713 main.whiley 2,15
  E730 main.whiley 2,15
  ====
  >>> main.whiley 5:6
    assume f(2,1) == 2
    assume f(2,2) == 4
  ---
  E730 main.whiley 2,15
  =====
  >>> main.whiley 1:2
  function f(int x, int y) -> int
  requires y >= 0:
  ---
  ``` 
  This test proposes an initial file `main.whiley` that should
  produce errors `E713` and `E730` upon compilation.  Then, in the next
  frame, the file is updated by replacing line `5` with two lines ---
  after which a compile error (`E730`) should still be reported.  The
  final frame introduces a precondition to function `f` which prevents
  an error being reported that `y` could be negative in `x ** y`.  See
  also {{<rfc id="110" name="0110-test-file-format">}} for a more in depth
  discussion.

* **Array/Record Update Operator** ({{<issue id="1129">}}).  The
  _array update_ `xs[x:=y]` and _record update_ `r[f:=x]` operators
  have been added for use within specification elements
  (e.g. `requires` clauses) and `property` declarations.

* **Unsafe Syntax** ({{<issue id="1093">}}).  A new modifier `unsafe`
  is now supported, though some questions remain over its semantic.
  Currently, it indicates that a `function` or `method` should not be
  verified (hence, it is unsafe).  Calling `unsafe` methods or
  functions does not require the caller is `unsafe`.  However, a
  `strict` mode can be enabled which does enforce this stricter
  requirement.

* **Bug Fixes** (e.g. {{<issue id="1132">}}, {{<issue id="1142">}},
  {{<issue id="1128">}}, {{<issue id="1120">}}, {{<issue id="1103">}},
  {{<issue id="1101">}}, {{<issue id="1097">}}, {{<issue
  id="1098">}}).  As usual there have been plenty of bug fixes, and
  I've only included a sample of them to the left.

