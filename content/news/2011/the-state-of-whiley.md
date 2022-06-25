---
date: 2011-07-26
title: "The State of Whiley"
draft: false
---

The aim of this post is simply to list the main outstanding issues with the design and implementation of Whiley.  This is primarily for my own purposes, in order to help me focus my efforts and to ensure I don't forget something important.
## Syntax
Deciding upon the language syntax is obviously the highest priority for me right now.  Over the last six months, a lot of the syntax has been locked down.  However, there remains a number of issues (some of which are thorny).
   * **Message Send Syntax**. Currently, the syntax for sending messages to actors is not finalised.  [This post](http://whileydave.com/2011/06/28/disambiguating-ambiguous-syntax/) provides all of the interesting details.

   * **Implicit Coercions**. These are causing me something of a headache as, in the context of structural subtyping, they're quite tricky.  [This post](http://whileydave.com/2011/07/21/implicit-coercions-in-whiley/) provides some insight into the problem, as does [this post](/2011/07/07/whiley-v0.3.7-released/).

   * **Default Imports.** Currently, like Java, every Whiley source file implicitly imports `whiley.lang.*` which (I think) is a bad idea.  The reason for this is that it doesn't make sense to unnecessarily clutter the namespace of every source file.  On the other hand, it is annoying to have to include that import explicitly, as most files will probably want it.

   * **Imports**.  Currently, when you import a module, all names from that module are imported directly.  For example, suppose a module `String` contains a function `indexOf()`.  The statement `import String` will import the name `indexOf` directly into our namespace.  This is convenient, but opens up potential for name clashes.  It might be better for `import String` to import the name `String.indexOf` rather than just `indexOf` (like Python).

   * **Encapsulation**.  Currently, there is no real support for encapsulation modifiers (e.g. `public`, `private`, etc). I plan to support `public` and `private` in the obvious ways.  However, I also want a third option.  Consider the definition `public define Rec as {int x}`.  This makes the name *and its contents* visible to clients.  But, I also want to be able to export the name *without its contents*.  The two options I'm considering are: using `protected` for this to be used in place of `public`; or, providing a special `export` declaration.  The idea of the latter is that, for a `private` type, we can declare something like `export Rec` --- this just makes the name `Rec` visible to clients, and nothing else.  I'm leaning towards `protected` as it's simpler, but it would cause some confusion with the meaning of `protected` in other languages.

   * **Interface Syntax.** Currently, there is no way to declare an `interface`, such as e.g. `Reader` in Java.  This is a serious deficiency which I will rectify as soon as I figure out the best way of doing it.

   * **Bindings.** Currently, every function or method compiled to JVM Bytecode has its name mangled ... which makes it impossible to call such functions/methods from native Java.  I am considering providing a "binding" modifier for methods/functions.  This would ensure a version of the method/function existed which was unmangled.

   * **Entry Point.** Currently, the entry point for a Whiley program is `void System::main([string] args)`.  This is problematic as it means that, until the main method exits, no actor can send a message to the `System` process.  One option is to support "headless" methods in Whiley --- then, the signature would become e.g. `void ::main(``System sys, ``[string] args)`.  In fact, the command-line arguments could be held in `sys` to further simplify this.

   * **Currying**. Currently, you can take the address of a function (e.g. `&f`).  However, you cannot curry functions.  So, I'd like to support syntax such as e.g. `&f(2,_)`, where the underscore indicates the actual parameter.

   * **Actor Fields.** Currently, you do not need to provide `this` when reading a field from `this` actor (unless a local variable of the same name already exists).  However, when assigning fields you do need to provide `this` ([this post](http://whileydave.com/2010/10/05/field-resolutio-in-whiley/) discusses why)  Likewise, you currently need to provide `this` when making an internal message send (however, I could infer it in most cases).  I'm wondering whether or not requiring `this` in all cases would be more a uniform approach, and give better readability.

   * **String Conversions**.  Currently, the system does not implicitly convert data types into strings.  Instead, you must explicitly call `str()`.  For example, to print an integer `i`, you would write `out.println(str(i))`.  This seems a little cumbersome, and somewhat unnecessary.

## Implementation
The current implementation targets the Java Virtual Machine and, for the most part, is in good shape.  However, there are a number of outstanding issues.
   * **Type System**.  My work on formalising Whiley's type system has thrown up a number of interesting issues.  In particular: types are not currently represented in a canonical fashion; they do not support distributivity across records/function types; and, ideally, they would include intersection and negation as first-class components.

   * **Dictionary and String Iteration**.  You cannot at the moment iterate over dictionaries or strings using the for loop.  This is a minor issue to fix.

   * **Break/Continue Statements**.  Break and continue statements are only semi-working right now.  Again, only a minor issue.

   * **Exceptions**.  At the moment you can `throw` exceptions, but you cannot `catch` them!  This should be easy to fix.  I need to consider whether or not a `finally` block is required.

   * **Actors**.  At the moment, Actors are currently implemented using a single `Thread` per actor.  This is highly inefficient, and eventually we will support *green threads*.

   * **Native function/method declarations**.  I will provide a `native` modifier for functions/methods to indicate they are provided by the system.

   * **Whiley Bytecode File Format**.  There is no binary file format for wyil files.  Thus, all signature information is currently stored directly in the Java classfile.  Eventually, however, such information will be stored in a binary wyil file (similar, in some ways, to a header file in C).  Then, the WHILEYPATH will only be searched for wyil files, not Java classfiles.  The primary reason for this is to support compilation to non-JVM targets, such as machine code.****

   * **Record Access Bytecode**s. Currently a record access requires a specific type (i.e. `Type.Record`) which is generated from `effectiveRecordType()`.  This is  a problem as the back-end loses knowledge of the actual representation of types.  For example, `{int x}|{[int] x}` is converted by `effectiveRecordType()` into `{int|[int] x}` to be stored in a `FieldAccess` bytecode.  This presents a problem if {int x} is represented differently from `{int|[int] x}` (which it might be in the case of `int` being implemented using a native `int`).


And, of course, there are quite a few outstanding bugs yet to be fixed!
## Performance
Performance is a significant issue in Whiley at the moment.  It's unlikely that this will change in the near future, however eventually I will address it.  There are currently three main techniques that I will use to address this:
   * **Reference Counting**.  Here, the idea is that every compound structure (e.g. a list) maintains a reference count.  Then, when an update is made to a compound structure, the count is checked.  If its `> 1` the structure is cloned; otherwise, the update occurs in place.  See [this paper](http://www.sable.mcgill.ca/mclab/mcvm/mcvmcc2011.pdf) for more on how this might work.

   * **Integer Range Analysis**.  A significant challenge in Whiley (from a performance perspective) is that the `int` type represents *unbounded integers* which are currently implemented as a `BigInteger`.  However, when possible, we want to use native JVM ints.  In order to do this, I propose using an integer range analysis to determine the lower and upper bounds of a given type.  This would be performed intra-procedurally and, in conjunction with pre/post-conditions, it should be very effective.  See [this link](http://user.it.uu.se/~svenolof/IRA01/) for relevant papers.

   * **Native Lists/Sets**.  Currently, lists of e.g. bytes are implemented as e.g. `ArrayList<Byte>`.  This is not efficient and I want to provide specific list implementations which (in this case) would use `byte[]` internally.

   * **Representation of Records.** Currently records are represented by `HashMap`.  However, it would be more efficient to represent them as `Object[]`, giving guaranteed constant-time lookup.

   * **Tagged Unions**.  In some cases, a tagged union could speed up runtime type tests.

