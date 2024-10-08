# xlisp-for-xenix-and-att-systemv
XLISP(-PLUS) by David Betz and Tom Almy adjusted to compile on ancient Unix

TL;DR: you need xl21gtar.img, which is a tar-archive, extended with binary zeroes up to standard 1.44MB diskette size.

--------------

Background & Details

I wanted "a free Lisp for Unix".

From some site with contents similar to these here:

https://www.cs.cmu.edu/afs/cs.cmu.edu/project/ai-repository/ai/util/lang/lisp/impl/

... I got all sorts of XLISP-variants, which, over the years, I stitched together in a most frankensteinesque fashion. However, the result should allow to be "made" both under Xenix 386 and under AT&T Unix System V Release 4 (SVR4) without any difficulty.

For "more regular" XLISP versions, documentation, etc, certainly:

https://almy.us/

... is highly recommended.

What to do: the image files are actually tar archives, but not compressed. I.e. in the ancient Unix of your choice, you can go into a directory, and e.g. do:

dd if=/dev/dsk/f0 of=a.tar

for AT&T Unix SVR4, or, for Xenix:

dd if=/dev/rfd0 of=a.tar

Then, you can uncompress the tar file thus obtained:

tar xivf a.tar

and you will get the image uncompressed. For xenix, within xl21gtar.img, there is a precompiled xlisp.xnx-file.

xl21gtar.img should normally have its c-files within a directory "sources" under the tree given by xlmini.img. You do not need xlmini.img, it is, so to say, the "unused rest" in compiling XLISP, but has been included for the sake of completeness. Also, in AT&T SVR4 I clashed with a very weird bug: xlprin.c was not being extracted correctly. So I created another image, xlprintar.img, which only contains SEVERAL copies of xlprin.c, in the hope at least one of them to be extracted correctly, so as to be pasted inside the source tree of xl21gtar.img (you shall extract it elsewhere, and copy it there manually), and to allow compilation. That seems to work.

My deep gratitude goes to David Betz and Thomas Almy, and all their helpers, for having created this amazing piece of software in the first place.

--------------

Update: added the Xenix-2.3.1-compiled binary of the LISP system, "xlisp.bin". This will also run under other Unix System V variants such as Unixware 1.0. The floppy image contains xlisp.bin "placed onto binary zeroes, up to the size of a standard 1.44MB floppy". You can then "insert" the "floppy" into your emulator and "dd" the binary straight from it, with something like:

dd if=/dev/dsk/f0 of=xlisp bs=128 count=2453



