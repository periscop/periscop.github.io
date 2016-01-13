---
layout: page
title: Clay
permalink: /clay/
---

## Introduction

Clay leverages the polyhedral model to perform complex program transformations expressed by high-level directives.

Polyhedral model offers an exceptional power of analysis for optimization of subclasses of imperative programs, but its internal representation is difficult to use even for the experts and is disconnected from the syntactic representation of the program, i.e. the source code.  Clay provides a mapping from source-level transformation directives to polyhedral constructs allowing the user to manipulate loops and statements and still benefit from the full power of the polyhedral analyses.  Many of these directives, such as loop fusion, distribution or tiling, are well known in the program optimization area.

Clay is a research prototype and may contain bugs.

CLAY stands for Chunky Loop Alteration wizardrY, _Chunky_ is the ancestor of the Periscop project.

## Downloads

Please use the latest development version while we prepare a stable release of Clay.  Prefer Git version as it uses submodules to download all the dependencies.

Download the development version: [clay.zip](https://github.com/periscop/clay/archive/master.zip).

You can also get it through Git: `git clone https://github.com/periscop/clay.git`.

## Installation

Clay depends on multiple other projects from the Periscop suite, namely OpenScop, CLooG, Clan and Candl.  Make sure they are installed and the installation paths are visible to either Make or CMake.  In git repository, you can call `./get_submodules.sh` to initialize and download the proper versions of the dependences.

### Make installation process

Clay may build with autotools as follows

```sh
./autogen.sh
./configure
make
make install
```

### CMake installation process

Alternatively, we provide a CMake installation process with the following recipe

```sh
mkdir build
cd build
cmake ..
make
make install
```

CMake library description is installed with Clay by default whatever build system you chose making it visible for other projects using CMake.

## Usage

Clay executive file comes with usage documentation available by calling `clay --help`.

By default, Clay takes an input file in the OpenScop format with an extension "Clay" that contains the sequence of transformations to perform.  It may also extract polyhedral representation from the C source code with `--readc` option and produce C coude with `--printc` option.  The combination of these options is abbreviated to `-c`.  The result is printed to the standard output.

When C code is given as input to Clay, the parts of the code subject to polyhedral extraction should be delimited by `#pragma scop`, `#pragma endscop` directives and satisfy requirements for static control imposed by Clan.  Clay directives should be put in a multi-line C99 comment, first line of which contains the word `Clay` as in

```c
  // ...
  some_function();
#pragma scop
  /* Clay
     transformation_1(parameters);
     transformation_2(parameters);
   */
  for ( ; ; ) {
    statement;
    // ...
  }
#pragma endscop
  some_other_function();
  // ...
```

Note that new lines in the multi-line comment should _not_ start with asteriscs.  The list of supported transformations directives and their syntax is provided by calling `clay --list`.

If the transformed program has the semantics different from the original program, Clay will output a violated dependnce graph instead of the transformed OpenScop format or C code.  The user may either fix the transformation to correct semantics or bypass dependence analysis by passing `--nocandl` option.  In the latter case, the transformed program is not guaranteed to be correct.

## Library

Clay transformation functionality is available in a library, `libclay`.  Include `clay/clay.h` and link against `-lclay` to access it.  Transformation functions (distribution, tiling, etc) may be called individually with prefix `clay_` or parsed from the C string and executed by `clay_parse_string(osl_scop_p, char *str, clay_options_p)`.  Clay uses OpenScop library data types for representing the program and its own data types for directives and their parameters.  Refer to the Doxygen documentation, which you can build with `make doc`, for more details.

## Contacts

Clay was initially developed by Joël Poudroux under supervision of [Cédric Bastoul](http://icps.u-strasbg.fr/~bastoul).  It was later heavily modified by [Oleksandr Zinenko](https://www.lri.fr/~zinenko) who is now maintaining the project.
