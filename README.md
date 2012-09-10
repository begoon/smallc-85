This fork from https://github.com/ncb85/SmallC-85 has no functional
changes, only a few build scripts.

- - -

Revived version of SmallC based on Chris Lewis' port to UNIX V. I have
mainly rewritten code to use structures and to make it compile using GCC
silently without warnigns.

Support for one line comments from C99 specification was added as well
as capability to handle Windows EOLs.

Initialisation of global variables is also possible. When not initialised
global var is assigned zero at compile time.

Furthermore support for ANSI style method declaration has been added.

Generated code is suitable for ASXXXX assembler/linker.

***** update *****
Support for unsigned types
Support for undocumented 8085 istructions LHLX, SHLX, LDSI, ARHL

-------------------------- original posting ------------------------------

Small C version C3.0R1.1
                              (SCC3)

                            Chris Lewis

This directory contains the source for a version of Ron Cain's Small C
compiler that I have heavily modified - beyond the Small-C V2.0 later
published in Dr. Dobbs.  This compiler generates assembler source code that
needs to be assembled and linked to make a running program.

Small C is a public domain compiler for a subset of C.  The main things
lacking are "#if", structs/unions, doubles/floats/longs and more than
one level of indirection.  Even so, it's powerful enough to be able to
compile itself.  It's also lots of fun to play around with.  It could
use lots of more work (eg: a real scanner), but what the heck...
Retargetting the compiler requires only relinking the frontend with a new
code generator.

Code generators for 6809 (MIT UNIX-like assembler), M68K (Motorola V/68
UNIX
assembler), VAX (BSD 4.1 assembler), and 8080 (RMAC assembler) are
provided.

Users having access to System V make should be able to use the Makefile
without any modification except for INCDIR and LIBDIR (where you'd like
to put the compiler itself).

Users not having access to System V will probably have to rewrite the
Makefile.
[ I have provided a Makefile that seems to work with bsd systems - mod]

WARNING: you will probably see a great deal of compilation warnings when
you compile this compiler with a "real" UNIX C.  Don't worry - this is
*perfectly* normal - Small C is a subset of real C, and in order to
keep the compiler in this subset you have to bend the rules somewhat.
The only time where this might cause a problem is where pointers are
"different" from ints (ie: different length or on non-byte-addressible
machines).  Small C assumes that ints are the same as pointers.

Invocation:
        scc<6809|vax|m68k|8080> filename

There are other options available - see main.c for details.

The code generated by these compilers need a run-time support library
for two things: operations that are "hard" on a particular processor
(eg: 16 bit multiply on an 8080), or O/S interface (vax is BSD 4.1,
6809 is FLEX, 8080 is CPM, never had one for M68k).

Status: the 6809, VAX and 8080 versions work last I checked - a problem or
two may have crept in during the implementation of the compile/assemble/and
link code for machines that support it.  The M68k version has never been
tested.  I don't have a Pyramid version because Pyrcorp seems reluctant
to publish instruction set information.

So you want to write a new coder do you?  Well, it's easy - read the
comments in one of the coders.  You should not have to modify *any* of
the existing files, just write a new codexxx.c file.  Please contact
me if you run into trouble.  I would be greatly interested in any new
coders or bug reports in the compilers.  As far as I am aware, the
major restriction on porting this thing for different targets is that
pointers and integers *must* be the same length, alignment, and be
interchangeable.