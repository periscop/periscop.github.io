---
layout: page
title: Chlore
permalink: /chlore/
---

## Introduction

Chlore is an implementation of the syntactic transformation recovery algorithm for a polyhedral optimizing compiler.

Polyhedral compilation uses a mathematical representation of specific parts of imperative programs to perform aggressive optimization.  However, polyhedral optimizer takes either code or mathematical representation as input and generates results in the same form, hard to understand for the end user.  Chlore allows to recover a sequence of syntactic primitives based on [Clay](http://periscop.github.io/clay) transformation set that achieve an equivalent transformation of the program.  This sequence may be read, understood and modified by the user and supplied to Clay for final code generation.

Chlore is a research prototype and may contain bugs.  Do not hesitate to [report them](https://github.com/ftynse/chlore/issues).

ChLORe stands for Chunky Loop Optimization Recoverer, _Chunky_ is the ancestor of the Periscop project.

## Downloads

No stable release of Chlore happened yet, the development version provided is subject to frequent changes.

Download the development version: [chlore.zip](https://github.com/ftynse/chlore/archive/master.zip).

You can also get it through Git: `git clone https://github.com/ftynse/chlore.git`.

## Installation

Chlore depends on other projects from the Periscop suite, namely [OpenScop](https://github.com/periscop/openscop), [Clay](https://github.com/ftynse/clay) and [CLooG](https://github.com/periscop/cloog).  The only external library required is [GMP](http://www.gmplib.org) which is available on multiple platforms.

Make sure you download and install the latest _development_ version of these tools and install them on your system.  Follow instructions available for each separate project.  Once installed, build Chlore with [CMake](https://cmake.org) as follows

```sh
mkdir build
cd build
cmake ..
make
make install
```

Make sure the installation paths of other projects are visible to CMake or use `-DCMAKE_PREFIX_PATH` option.

In case you need to uninstall Chlore, call

```sh
make uninstall
```

in the bulid directory.  Note that as newer versions of Chlore may install a different set of files, it is recommended to use the exact same source code version for the uninstallatio process.

## Usage

Chlore takes the original and the transformed programs in OpenScop representaiton as follows

```sh
chlore original.scop transformed.scop
```

The corresponding Clay transformation sequence is printed to the standard output.  Chlore may also include an OpenScop extension containing the transformation sequence to the original file if called with `--output-extension` options.

Call `chlore --help` for the list of available options in the current version.

## Library

Main functionality of Chlore is available as a library, `libchlore`, that is automatically built and installed.  Include `chlore/chlore.h` to your source code and call

```c
void chlore_whiteboxing(osl_scop_p original, osl_scop_p transformed);
```

which will add the recovered sequence as an osl extension `osl_clay_p` to the extension field of the original SCoP. `osl_scop_*` and `osl_clay_*` types are available from the OpenScop library and are described in its documentation.

You may need to link your project with `-lchlore -lcloog-isl -lisl -losl -gmp`.

## Citing

Chlore tool and algorithm were presented as a research [paper](https://hal.inria.fr/view/index/identifiant/hal-01253322/lang/en) at the CGO conference in 2016.

You may cite this paper as follows:

Lénaïc Bagnères, Oleksandr Zinenko, Stéphane Huot, Cédric Bastoul. Opening Polyhedral Compiler's Black Box. _CGO 2016 - 14th Annual IEEE/ACM International Symposium on Code Generation and Optimization_, Mar 2016, Barcelona, Spain.

## Contacts

The project is developed and maintained by [Oleksandr Zinenko](https://www.lri.fr/~zinenko).  Please report bugs, suggest changes or submit pull requests to the GitHub repository [https://github.com/ftynse/chlore](https://github.com/ftynse/chlore).

