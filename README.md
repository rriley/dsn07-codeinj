Intro
---

This is the source code related to my first research paper.  It involves low-level abuse of the TLB
on Intel processors.

The Paper
---

Ryan Riley, Xuxian Jiang, Dongyan Xu, [ "An Architectural Approach to Preventing Code Injection Attacks"](https://vsecurity.info/pubs/dsn07-codeinj.pdf), Proceedings of _IEEE/IFIP International Conference on Dependable Systems and Networks ([DSN-DCCS 2007](http://www.dsn.org/))_, Edinburgh, UK, June 2007.

The Code
---

This archive contains the code I used while working on the above 
mentioned paper.  This was my first real systems project, and as such I 
apologize in advance for some of the lackluster quality.  Anyone with a 
real background will quickly realize just how little I know about the 
Linux kernel.  I assure you, my abilities have grown since then.  Really.  
I think.  Anyway, here we go..

Kernel Compiling:
 - Get a copy 2.6.13 of the Linux kernel.
 - Apply the patch

This means you should do the following, or something similar:
 
```
wget https://www.kernel.org/pub/linux/kernel/v2.6/linux-2.6.13.tar.bz2
tar jxf linux-2.6.13.tar.bz2
cd linux-2.6.13
patch -p0 < ../dsn07.diff
make oldconfig
make
```

To activate the protection for a specific program, you need to use the 
wrapper program.  Compiling it is fairly straight forward, but it does 
depend on the unistd.h from the modified kernel in order to work.  (This 
gives it the information about the new system call number.)  After you 
manage to get it to compile, you can use it like...
```
./wrapper <program to protect> <args to program>
```

mirexp.c is a very simple program that runs code from somewhere it 
shouldn't.  With the protection on, the program should segfault.

If you are trying to use this for something and have trouble setting it 
up, let me know, I'll try my best to help you out.  Also, if you end up 
using this and find horrible flaws (I'm sure there are some) or fix some 
of the weird bugs mentioned in the code's comments, please let me know 
that as well.  There are numerous things about implementing this project 
that continue to mystify me, and I would love the chance to learn where 
I made my mistakes.  Also note that I've discovered that running this on 
a Pentium 4 (my test machine is a P3) may result in really strange 
slowdown.  PaX has noticed this same phenomenon.

Ryan Riley

