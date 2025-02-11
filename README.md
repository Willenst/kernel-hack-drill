# Linux kernel exploitation experiments

This is a playground for the Linux kernel exploitation experiments.
Only basic methods. Just for fun.

__Contents:__

  - __drill_mod.c__ - a small Linux kernel module with nice vulnerabilities. You can interact with it via a simple procfs interface.
  - __drill.h__ - a header file describing the `drill_mod.ko` interface.
  - __drill_test.c__ - a test for `drill_mod.ko`. It should also pass if the kernel is built with `CONFIG_KASAN=y`.
  - __drill_exploit_uaf_callback.c__ - a basic use-after-free exploit invoking a callback in the freed `drill_item_t` struct.
  - __drill_exploit_uaf_write.c__ - a basic use-after-free exploit writing data to the freed `drill_item_t` struct.

N.B. Only basic exploit techniques here.

So compile your kernel with `x86_64_defconfig` and run it with `pti=off nokaslr` boot arguments.

Also don't forget to run `qemu-system-x86_64` with `-cpu qemu64,-smep,-smap`.

License: GPL-3.0.

Have fun!

# Setup

Let's go over the steps for building and installing a kernel with a module, transferring and including it to a target machine, and troubleshooting version mismatch issues.

## Integrate drill in kernel sources

This method is not recommended because it would then be somewhat more difficult to dynamically work with the code

1. If already haven't - download the kernel sources
2. Put the module source in a folder in the kernel tree
3. Change the Makefile and Kconfig to include the module
4. Enable the module as build-in (for example use menuconfig)
5. Compile the kernel

## Deploy module to the target machine

For this method, you must first set up an ssh connection between your primary and target machines.

1. Module needs to be compiled, for doing so it must be placed in a kernel sources tree
* If your current kernel differs from tested one, KPATH in Makefile must be changed like that
`KPATH := ../` (or use your path to the kernel sources)
2. Use the folowing scp command to move compiled module to the kernel
3. (Optional) add ssh keys to the target machine for faster authentication

## Compile in a target machine

1. Install necessary build tools and kernel headers
2. Deliver hack drill via git or scp
3. Use Makefile to compile the module
4. use insmod to integrate the module

### Handling version missmatch issues
==(to be done)==

# Usage
==(to be done)==

## Repositories

 - At GitHub: <https://github.com/a13xp0p0v/kernel-hack-drill>
 - At Codeberg: <https://codeberg.org/a13xp0p0v/kernel-hack-drill> (go there if something goes wrong with GitHub)
 - At GitFlic: <https://gitflic.ru/project/a13xp0p0v/kernel-hack-drill>

[1]: https://bugs.chromium.org/p/project-zero/issues/detail?id=1792&desc=2
