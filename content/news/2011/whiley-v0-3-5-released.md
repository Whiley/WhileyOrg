---
date: 2011-05-08
title: "Whiley v0.3.5 released!"
draft: false
---

## ChangeLog

Separated compiler up into two main components as follows:
   
   * **The Whiley Compiler (wyc)**.  This provides a base compiler which is responsible for parsing whiley programs, as well as type checking and constraint checking them.  This outputs whiley bytecode (wyil) which can then either be executed directly, or compiled to some target platform (e.g. JVM)

   * **The Whiley-to-Java Compiler (wyjc)**.  This extends the base compiler in two ways: firstly, it supports compiling wyil code to jvm bytecode and provides an appropriate runtime;  secondly, it provides a mechanism whereby whiley programs can interface with Java libraries.


This now paves the way for other compiling whiley programs to other platforms (e.g. llvm).

   * In separating out the two main components of the compiler, I also added a generic mechanism for processing command-line arguments and constructing Whiley Compiler pipelines.  This probably needs more work, but it lets you easily construct a default pipeline and then add/remove/configure pipeline stages.

   * Changed message send syntax and implement thread-based Actors.  Firstly, synchronous message sends are distinguished from asynchronous ones using special syntax.  Thus, `out<->println(...)` is a synchronous message send, whilst `out<-println(...)` is an asynchronous message send.  Actors are now implemented using JVM threads, where each Actor corresponds to a single thread.  This is not an efficient approach, particularly as it won't scale up beyond a few hundred actors.  However, it's a useful stopgap to demonstrate the actor system and let me play with it.

   * Fixed numerous bugs
