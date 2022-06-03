---
date: 2011-02-14
title: "Whiley v0.3.3 Released!"
draft: false
---

This latest update of Whiley is a somewhat minor increment over the previous.  Aside from a number of bug fixes the main improvement is the inclusion of first-class functions (aka function pointers).  Constraint checking remains disabled, as it still needs a considerable amount of work (which I'm working on :)

Function pointers can be used like so:
```whiley
int f1(int x):
    return x + 1

int f2(int x):
    return x * 2

int g(int(int) func):
    return func(1234)
    
void System::main([string] args):
    out->println(str(g(&f1)))
    out->println(str(g(&f2)))
```
