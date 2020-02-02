Questions

## Bug Report!

Q: What is an excellent bug report you created at a previous company which was of a high priority, high severity in a build about to be deployed to production? (Please write the bug report below)


A:

** So, for privacy reasons I can not show reports for software I have worked on at my other jobs. 

However, I can point you to some dialogue I have had with FreeBSD developers and enthusiasts, which I think illustrates some of the detail oriented extrapolation you are seeking. 

For context, this issue had to do with compiling FreeBSD images for a Raspberry Pi. Unfortunately the Raspberry Pi platform is not considered tier 1, which means you can not update the operating system directly on the device itself. Instead, you have to compile your own image either using a build automation tool called Crochet, which through cross compiling magic produces an image for an embedded device of your choice, or you can set up your own cross compiling tool chain and do it yourself, which is what I was attempting to do. Basically using a tool called distcc, which distributes compilation jobs across a network, and running my Raspberry Pi in conjunction with a virtualized arm image on a much faster device, I was attempting to do a kernel upgrade.

In this report, I clearly state the issue I am having, the platform I am on, the tools I am trying to use, and the output of the error.

The error I was hitting was something in the libgcc toolchain, which meant I was in over my head, which is why I sought advice from more experienced users. Here is a detailed report of my issue: **

`Hi everyone,

I have installed the most recent image of 12.1 to my sdcard and I have an
identical image running under qemu. The release revision is @ 352868. I
have setup distcc successfully and compilation works, but it fails at this
point:

To be clear, I am compiling directly on the Pi itself and offloading jobs
to an arm qemu instance on a faster computer. As far as I know the images
running are the same.

/usr/src/gnu/lib/libgcc/../../../contrib/gcc/unwind-dw2.c:1396:3: error:
cannot compile this __builtin_init_dwarf_reg_size_table yet
  __builtin_init_dwarf_reg_size_table (dwarf_reg_size_table);
  ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
1 error generated.
distcc[74549] ERROR: compile
/usr/src/gnu/lib/libgcc/../../../contrib/gcc/unwind-dw2.c on localhost
failed
*** [unwind-dw2.o] Error code 1

make[4]: stopped in /usr/src/gnu/lib/libgcc
1 error

make[4]: stopped in /usr/src/gnu/lib/libgcc
*** [gnu/lib/libgcc__PL] Error code 2

make[3]: stopped in /usr/src
--- lib/libcompiler_rt__PL ---
A failure has been detected in another branch of the parallel make

make[4]: stopped in /usr/src/lib/libcompiler_rt
*** [lib/libcompiler_rt__PL] Error code 2

make[3]: stopped in /usr/src
2 errors

make[3]: stopped in /usr/src
*** [libraries] Error code 2

make[2]: stopped in /usr/src
1 error

make[2]: stopped in /usr/src
*** [_libraries] Error code 2

make[1]: stopped in /usr/src
1 error

make[1]: stopped in /usr/src
*** [buildworld] Error code 2

make: stopped in /usr/src
1 error

make: stopped in /usr/src

It seems a similar problem happened for someone in this StackOverflow
thread,
https://stackoverflow.com/questions/53786496/clang-error-cannot-compile-builtin-function-yet.
However this person was compiling the Linux kernel and it looks like they
used GCC to get around the issue, which I don't think I can do here?`

**Additionally, I have submitted small patches to some projects I am interested in. https://reviews.freebsd.org/rP491573 is an example of a patch submitted on my behalf by a port maintainer on FreeBSD. I reached out to the maintainer directly and provided him the patch. This patch fixed a run time error in the quarterly version of a package used for remote streaming. I tracked down the issue by following threads in the upstream's git repo.** 

## Bug Report Follow up

Q: For the created bug report example you created in the previous question, what happened and how did you navigate the bug lifecycle, bug discussion? 

A: 

**Luckily, some people were more than happy to help. Unfortunately, a solution was never found, because the person interested was on a different revision and instead of duplicating my setup, they did their upgrade directly on the device, which according to them took roughly 30 hours. That wasn't something I wanted to do. You can view the full thread here with their feedback: https://lists.freebsd.org/pipermail/freebsd-arm/2019-September/020495.html . Ultimately, I am awaiting tier 1 support, which there is a growing demand for, so I am glad to have used their mailing lists to add my voice to the discussion.** 
