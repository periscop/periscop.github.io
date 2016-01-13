---
layout: default
---

Periscop suite aggregates a set of tools and libraries for using the polyhedral model (or polytope model) in an optimizing compiler.

Polyhedral model uses an algebraic representation of imperative program statements and control constructs to provide deep analysis and enable agressive restructuring.  From the very high-level point of view, iterative executions of program statements are represented as points in a multi-dimensional space that form a polyhedron, hence the name of the system.  This representation was initially available only for static control flow regions, commonly referred to as SCoP, Static Cotrol Parts.  This periscop means tools "around static control flow parts".

The suite currently contains the following projects:

[OpenScop](https://github.com/periscop/openscop): representation format for polyhedra and an exchange library;
[PipLib](https://github.com/periscop/piplib): parametric integer programming solver library, the mathematical core behind the polyhedral optimization;
[CLooG](http://www.cloog.org): code generator from the polyhedral representation;
[Clan](https://github.com/periscop/clan): polyhedral representation extractor from the C code;
[Candl](https://github.com/periscop/candl): data dependence analyzer in the polyhedral model;
[Clay](/clay/): source-level semi-automatic program transformation engine;
[Chlore](/chlore/): tool for reverse engineering the effects of polyhedral optimization on the source level.

