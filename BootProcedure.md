# Boot Procedure in Linux

The boot procedure in Linux involves a series of steps that the system follows to load the operating system and reach a usable state.


## 1. BIOS Stage

- When the machine is powered on BIOS is the first one to be called to verify if the hardware is present in the machine and if it is functioning.
- This is done by performing a Power On Self Test (POST)
- After a successful test, BIOS checks the MBR (Master Boot Record) in the hard disk to check if it refers to the location of the boot loader.

## 2. Boot Loader Stage

The boot loader will be installed if an operating system is installed on the system.
Two of the most common boot loaders are:

- LILO (Linux Loader)
- GRUB (Grand Unified Boot Loader)

The boot loader will present the user with a list of menu entries, each of which corresponds to a different operating system.
The boot loader will then start to boot the operating system. When you select the option to start Linux, it decompresses the Linux kernel in memory.
After that Linux kernel (which you selected to boot from) loads initrd (Initial ramdisk). The initrd is used by the Linux kernel as a temporary filesystem in memory. It contains tools and kernel modules that will continue the boot process, including mounting a virtual root file system temporarily.
Instead of using initrd, some Linux filesystems will also use initramfs. It serves the same purpose as initrd, it is just that it is a successor of initrd.
Linuxrc is an executable file that is next spawned, it probes the mass storage hardware and finds a suitable kernel module to drive the mass storage hardware.
This is required to prepare the real root filesystem to be mounted by the Linux kernel.

## 3. Kernel Stage

In the kernel stage of the Linux boot sequence, the Linux kernel, based on the result of linuxrc, can then mount the real root file system.
The real root file system in Linux is referenced as "/", and it is where all other subdirectories and files visible when Linux is running exist.
The kernel will then spawn the init process, this process always has the process identifier (PID) as "1" because it is the first background process or daemon started by the kernel upon boot. All other background daemons are spawned from the init process. So the init process will load other system daemons depending upon the configuration of different runlevels.
For example:
If the system boots into runlevel 3, then the init process will start all the daemons from this runlevel.

