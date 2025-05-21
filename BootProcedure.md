# Boot Procedure in Linux

The boot procedure in Linux involves a series of steps that the system follows to load the operating system and reach a usable state.


## 1. BIOS Stage

- BIOS (Basic Input/Output System) is the firmware embedded on the motherboard.
- When the machine is powered on, the BIOS is the first one to be called to verify whether the hardware is present and if it is functioning.
- This is done by performing a Power On Self Test (POST)
- After a successful test, BIOS checks the MBR (Master Boot Record) in the hard disk to check if it refers to the location of the boot loader.

## 2. Boot Loader Stage

The boot loader will be installed if an operating system is installed on the system.
Two of the most common boot loaders are:

- LILO (Linux Loader)
- GRUB (Grand Unified Boot Loader)

- The bootloader:

   - Presents a boot menu (if multiple OSes are installed).

   - Loads the Linux kernel (usually a vmlinuz file).

   - Loads the initrd (initial RAM disk), which contains drivers and tools needed for booting. The initrd is used by the Linux kernel as a temporary filesystem in memory. It contains tools and kernel modules that will continue the boot process, including temporarily mounting a virtual root file system.

   - Instead of using initrd, some Linux filesystems will also use initramfs. It serves the same purpose as initrd, it is just that it is a successor of initrd.

   - Linuxrc is an executable file that is next spawned, it probes the mass storage hardware and finds a suitable kernel module to drive the mass storage hardware.
This is required to prepare the real root filesystem to be mounted by the Linux kernel.

## 3. Kernel Stage

- The kernel:

  - Decompresses and loads into memory.

  - Initializes hardware via built-in or loaded drivers.

  - Mounts the root filesystem. i.e., In the kernel stage of the Linux boot sequence, the Linux kernel, based on the result of linuxrc, can then mount the real root file system. The real root file system in Linux is referenced as "/", and it is where all other subdirectories and files visible when Linux is running exist.

  - Starts the init process (PID 1), which is the first user-space program. The kernel will then spawn the init process, this process always has the process identifier (PID) as "1" because it is the first background process or daemon started by the kernel upon boot. All other background daemons are spawned from the init process. So the init process will load other system daemons depending upon the configuration of different runlevels.
For example:
If the system boots into runlevel 3, then the init process will start all the daemons from this runlevel.

## 4. init or systemd Starts

- On modern Linux systems, systemd is the most common init system.

- It is responsible for:

  - Mounting file systems.

  - Starting system services (sshd, network, cron, etc.).

  - Setting hostname, time, and user sessions.

## 5. Login Prompt or Display Manager

- The system reaches:

  - A command-line login prompt (runlevel 3 or multi-user.target).

  - Or a GUI login screen (runlevel 5 or graphical.target).

- After login, a shell or desktop environment is launched.

