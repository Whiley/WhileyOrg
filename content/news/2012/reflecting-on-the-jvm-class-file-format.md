---
date: 2012-08-06
title: "Reflecting on the JVM Class File Format"
draft: false
---

The [latest release of Whiley (v0.3.16)](/2012/07/31/whiley-v0.3.16-released/) includes (finally) a binary file format for the Whiley Intermediate Language (WYIL).  You can think WYIL files are to Whiley, as [class files](http://en.wikipedia.org/wiki/Java_class_file) are to Java, or [CIL files](http://en.wikipedia.org/wiki/Common_Intermediate_Language) are to C#.  Furthermore, the existence of WYIL files implies there is a corresponding (albeit currently hypothetical) Whiley Virtual Machine (WYVM) which can execute them directly.  Developing this VM file format has been an interesting experience, and caused me to consider: *what makes a good VM file format? *
**
Without doubt, the JVM class file format was my main influence when developing the binary WYIL file format (rather than e.g. [CIL](http://en.wikipedia.org/wiki/Common_Intermediate_Language) or [LLVM BitCode](http://llvm.org/docs/BitCodeFormat.html)).  This is simply because I've spent a lot of time working with JVM class files and Java Bytecode in the past. But, there seem to be some obvious goals for any modern VM file format:
   * **Quick** to decode and verify in order that the VM can start up as quickly as possible.

   * **Compact** to minimise costs associated with e.g. network transportation.

   * **Scalable** so that we are not restricted to some maximum file size.

   * **Extensible** so that we can embed additional information as the language evolves, or for other non-computational purposes (e.g. embedding documentation or licenses).


In my opinion, the JVM class file format does a reasonable job --- but, it clearly falls short in a number of areas.  The presence of [attribute blocks](http://docs.oracle.com/javase/specs/jvms/se7/html/jvms-4.html#jvms-4.7) in the format means it is very extensible.  However, many important values are encoded using fixed-width unsigned integer values (e.g. as `u8`, `u16`, etc).  This has led to annoying limitations on the maximum size of various things (e.g. that a [code attribute cannot exceed 64KB](http://docs.oracle.com/javase/specs/jvms/se7/html/jvms-4.html#jvms-4.9.1)).

Anyway, here are a few more interesting thoughts I had about JVM class files:
   * **The format needed to be more resilient to large class file sizes**. In particular, using fixed-width integers at key positions was an inherently bad idea.  LLVM Bitcode has a better solution where arbitrary sized integers are [encoded using 4-bit nibbles where the high bit signals if another nibble follows or not](http://llvm.org/docs/BitCodeFormat.html#id14).

   * **The constant pool should have been stratified**.  That is, where pool items of the same kind are located together rather than being potentially located anywhere in the pool.  This is useful as, in many situations, we know what kind of pool item to expect (e.g. a `getfield` bytecode always refers to a [CONSTANT_Fieldref_Info](http://docs.oracle.com/javase/specs/jvms/se5.0/html/ClassFile.doc.html#42041) pool item).  In such situations, smaller index values could be used (i.e. which are offset from the start of the group, rather than the whole pool).

   * **Types should have been fully embedded into bytecodes**.  Since only partial type information is embedded in JVM class files, the bytecode verifier must recover the missing information (which is expensive, and the reason why the [StackMapTable](http://docs.oracle.com/javase/specs/jvms/se7/html/jvms-4.html#jvms-4.7.4) is now a required attribute).

   * **Bytecode branch offsets should not be in bytes.** Storing branch offsets in bytes (e.g. for bytecodes such as `goto`) makes sense when bytecodes are interpreted "in place" --- that is, when the interpreter does not expand them into an array of e.g. Bytecode objects, but instead interprets the raw bytes directly.  But, I don't think many interpreters would do this.  That's because decoding bytecodes is relatively expensive, and so it makes sense to carry this cost once and expand them into more easily managed objects.  In such case, it makes much more sense for branch offsets to be given in terms of whole bytecodes, rather than individual bytes.  This increases the range of a given branch, and also simplifies encoding since we avoid any difficult algorithms for computing branch offsets

   * **Register-based bytecodes instead of stack-based bytecodes**.  More modern bytecode formats (e.g. [LLVM BitCode](http://llvm.org/docs/BitCodeFormat.html) and [Dalvik Bytecode](http://en.wikipedia.org/wiki/Dalvik_%28software%29)) tend to prefer register-based bytecodes over stack-based ones.  This is partly because it's generally [easier to generate more efficient low-level machine code](http://nhc98.blogspot.co.nz/2006/05/register-based-bytecode.html) when starting from a register-based format.  Personally, I also find that code for manipulating register-based bytecodes is simpler and more robust.  This is because, with a stack-based format, one must always be very careful to maintain stack consistency.

   * **Issues of architecture and implementation should not have leaked into the file format**.  The most obvious example is the need for two register/stack slots when storing `long` and `double` primitives.  Likewise, the need to word-align switch bytecodes is just plain wierd.


Anyway, those are my thoughts!  And, I'm sure there are plenty of other design issues people have encountered ...
