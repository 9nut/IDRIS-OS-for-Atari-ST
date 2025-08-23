# Idris OS for the Atari ST
This repo contains Whitesmiths Ltd (now defunct) Idris OS version 3.12 for the Atari ST.
The porting work was done by **David M. Stanhope** at Computer Tools (also defunct), in 1986.
He also ported MIT's X Windows 10R4 to the ST. The work included ST specific device drivers
as well as pseudo drivers to support network (e.g. sockets, select).

## Distribution Manifest
The distro includes the following:
1. Boot disk (`boot.st`)
2. OS Distro disks (`dist?of2.st`)
3. Compiler disks (`compiler?of2.st`)
4. The kernel build disk (`kernbuild.st`)
5. X10R4 disks (`st_xwin10r4_?of4.st`)
6. Tar file floppies containing miscellaneous open source apps ported to Idris (`misc_*.st`)

## Running on Hatari
Idris runs on the 520 ST and the 1040 ST, as well as the MegaST. To run X10R4 use the
MegaST emulation with 4MB of memory.

To run the system on Hatari, set `Drive A:` from Floppy menu to the boot disk image and
rest the machine. At the "device number: " prompt, press `0` followed by enter. Then
enter `idrisk1a` at the `cboot` prompt and press enter. The system default is to
boot from the hard drive (device number 1), if the user input times out.

Once Idris is loaded, the shell is started and the `#` prompt will appear. Some Idris
commands are included on the boot floppy to allow bootstrapping the system onto a hard
drive.

## Hard Disk Installation
Hatari ACSI hard disk emulation doesn't seem to agree with Idris's ACSI driver. Idris is known
to work with real Atari ACSI disks such as the SH205.  Normally the `BuildHard` script would be
used to create a filesystem on the 3rd partition of the hard drive (`/dev/hdroot`). The
1st partition corresponds to `/dev/hdboot`, and the 2nd partition to `/dev/hdswap`. `BuildHard`
requires the number of sectors in `/dev/hdroot` partition for the `mkfs` command.

Using only the boot floppy, the other floppy images can be inspected by mounting them
on Drive B. Set Drive B to point to an image (e.g. `dist1of2.st`), then mount the second
floppy by:
```sh
# mount -r /dev/fd1 /y
# ls -l /y
...
# mount -u /y
```
The `-r` flag signifies _read-only_, and the `-u` flag is equivalent to _umount_.

Once `BuildHard` is able to run successfully, it will create the hard disk partition, create
the basic file system hierarchy and copy a few commands and will prompt the user to reboot
and select to boot from the hard disk (i.e. `device number: 1`).  Once Idris can boot
from the hard drive, the `Install` scrip will guide the user through the installation
process.

# Good Luck
