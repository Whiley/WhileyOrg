---
date: 2011-09-20
title: "The Whiley Automata Library (WYAUTL)"
draft: false
---

As part of the upcoming v0.3.10 release of Whiley, I've invested considerable effort reimplementing the type system.  This was necessary because, whilst my old implementation generally worked, writing larger programs exposed a lot of issues.  The most interesting aspect of this process is the development of a general-purpose library for representing and manipulating [tree automatas](http://whileydave.com/2011/07/06/regular-tree-automata/).
## Tree Automata
A tree automaton in WYAUTL is a directed graph where edges may have labels.  In general, the nodes of this graph are called *states*, whilst the edges are called *transitions*.  States have the following properties:
   * **Kind**.  Every state has a "kind", which tells us something about it.  States with the same kind are somehow related and should be treated in the same way.  In Whiley, each distinct category of type has its own kind.  For example, `void`, `any` and `null` are distinct kinds.

   * **Children.** Every state has zero or more children.  Essentially, the children of a state are those states directly reachable in a single transition.

   * **Determinism.** Every state is either *deterministic* or *non-deterministic*.  This choice affects the way states are treated within the various algorithms.  Essentially, in a non-deterministic state, there is no fixed ordering of children.  In a deterministic state, every child is in a fixed position and can only accepts inputs in that position (more on this later).

   * **Supplementary Data.** A state may additionally have some supplementary data.  This is specific to the problem domain the automata are used for.  In Whiley, for example, states corresponding to records have supplementary data to store field names.


A tree automaton *accepts* matching *input trees*.  An input tree is essentially an acyclic automaton (generally speaking a tree, although it doesn't actually need to be).   Tree states have kinds, children and (optionally) supplementary data.  However, tree states are always deterministic.  The intuition is that an automaton state matches a tree state if they have the same kind, and their children match as well.  The issue of determinism and supplementary data make this picture slightly more complicated, however.
## Example
To begin with, I'll consider an entirely abstract example.  This is because the automata library can represent arbitrary tree automata, not just those needed to for types in Whiley.  Then, we'll see how this translates into the underlying representation of types in Whiley.

{{<img class="text-center" width="75%" src="/images/2011/TreeAutomata.png">}}

In this example, we have a single automaton on the left, and three matching tree inputs on the right.  In the automaton, square nodes indicate deterministic states, whilst circles indicate non-deterministic states.  The kind of a state is given by its colour.  We can see, for the deterministic states, that every transition is given a numeric label.  This indicates the "position" of that transition and, for simplicity, can be thought of as an edge label.  In the tree inputs, every node is deterministic and, hence, all transitions are labelled.

In the above example, a deterministic state in the automaton matches a state in an input tree if they have the same kind, and each child matches the corresponding child in the input.  For the non-deterministic states, however, it's sufficient that, for every child state of the input, there exists a matching child state in the automaton.
## Back to Types
Types in Whiley are represented using tree automata.  In fact, if you look at my previous posts on the algorithmic aspects of implementing types in Whiley  (see e.g. [here](http://whiley.org/2011/08/30/simplification-vs-minimisation-of-types-in-whiley/), [here](http://whiley.org/2011/03/07/implementing-structural-types/) and [here](http://whiley.org/2011/02/16/minimising-recursive-data-types/)) you'll notice a striking resemblance with the above diagrams.  That's because, well, they're essentially the same.  Take, for example, the following Whiley type:

```whiley
define Tree as null | {int data, Tree left, Tree right}
```

The above type can be represented as a tree automaton, like so:

{{<img class="text-center" width="75%" src="/images/2011/TreeAutomata2.png">}}

Here, grey states represent `null`, yellow states represent `int`, blue states represent `records` (i.e. `{ ... }`) and green states unions (i.e. `... | ...`).  Furthermore, the rules for accepting inputs are adjusted so non-determinstic states do not themselves need to match a corresponding state in the input (although their children still do).  The latter is made possible in the library because one can extend the "default interpretation" of automata.
## Conclusion
Overall, implementing a general purpose automata library has proved successful in reducing complexity of the Whiley compiler.  This is because the library abstracts many of the key differences between types, and handles various issues such as *minimisation* and *canonicalisation* automatically. The library can also be developed and tested in isolation, making it easier to focus on without getting distracted by Whiley specifics.