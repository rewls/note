# Raspberry Pi in QEMU

- Arch Linux

```sh
# pacman -S qemu-system-aarch64
```

- [Raspberry Pi operating system images][raspios]

## Raspberry Pi OS Bullseye

- Release date: October 22nd 2024

- System: 32-bit

- Kernel version: 6.1

- Debian version: 11 (bullseye)

```sh
$ wget https://downloads.raspberrypi.com/raspios_oldstable_armhf/images/raspios_oldstable_armhf-2024-10-28/2024-10-22-raspios-bullseye-armhf.img.xz
$ xz -d 2024-10-22-raspios-bullseye-armhf.img.xz
```

```sh
$ file 2024-10-22-raspios-bullseye-armhf.img
2024-10-22-raspios-bullseye-armhf.img: DOS/MBR boot sector; partition 1 : ID=0xc, start-CHS (0x40,0,1), end-CHS (0x3ff,3,32), startsector 8192, 524288 sectors; partition 2 : ID=0x83, start-CHS (0x3ff,3,32), end-CHS (0x3ff,3,32), startsector 532480, 7872512 sectors
```

```sh
$ fdisk -l 2024-10-22-raspios-bullseye-armhf.img
Disk 2024-10-22-raspios-bullseye-armhf.img: 8 GiB, 8589934592 bytes, 16777216 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x2bc2872b

Device                                 Boot  Start     End Sectors  Size Id Type
2024-10-22-raspios-bullseye-armhf.img1        8192  532479  524288  256M  c W95 FAT32 (LBA)
2024-10-22-raspios-bullseye-armhf.img2      532480 8404991 7872512  3.8G 83 Linux
```

```sh
$ bc
512*8192
4194304
```

- [mount(8)][mount], [losetup(8)][losetup]

```sh
# mkdir /mnt/raspios-bullseye
# mount -o offset=4194304 2024-10-22-raspios-bullseye-armhf.img /mnt/raspios-bullseye
```

- [Raspberry Pi Docs > Computer > Configuration][raspi conf]

```sh
$ cp /mnt/raspios-bullseye/bcm2708-rpi-zero-w.dtb .
$ cp /mnt/raspios-bullseye/kernel.img .
```

- [Raspberry Pi Docs > Computer > Configuration][raspi conf]

```sh
$ openssl passwd -6
```

```sh
$ echo '<username>:<password>' | sudo tee /mnt/raspios-bullseye/userconf.txt
```

- [Raspberry Pi Docs > Computer > Configuration][raspi conf]

- [QEMU Docs > System Emulation > QEMU System Emulator Targets > Arm System emulator][arm emul]

- [QEMU Docs > System Emulation > Invocation][invoc]

```sh
$ qemu-system-aarch64 -machine raspi0 \
    -sd 2024-10-22-raspios-bullseye-armhf.img \
    -nographic \
    -kernel kernel.img \
    -append "console=ttyAMA0,115200 \
        root=/dev/mmcblk0p2" \
    -dtb bcm2708-rpi-zero-w.dtb
WARNING: Image format was not specified for '2024-10-22-raspios-bullseye-armhf.img' and probing guessed raw.
         Automatically detecting the format is dangerous for raw images, write operations on block 0 will be restricted.
         Specify the 'raw' format explicitly to remove the restrictions.
qemu-system-aarch64: Invalid SD card size: 4.01 GiB
SD card size has to be a power of 2, e.g. 8 GiB.
You can resize disk images with 'qemu-img resize <imagefile> <new-size>'
(note that this will lose data if you make the image smaller than it currently is).
```

```sh
$ qemu-img resize 2024-10-22-raspios-bullseye-armhf.img 8G
```

```sh
$ qemu-system-aarch64 -machine raspi0 \
    -sd 2024-10-22-raspios-bullseye-armhf.img \
    -nographic \
    -kernel kernel.img \
    -append "console=ttyAMA0,115200 \
        root=/dev/mmcblk0p2" \
    -dtb bcm2708-rpi-zero-w.dtb

```

- Not booting

- [Raspberry Pi Docs > Computer > Configuration][raspi conf]

```sh
$ qemu-system-aarch64 -machine raspi0 \
    -sd 2024-10-22-raspios-bullseye-armhf.img \
    -nographic \
    -kernel kernel.img \
    -append "console=ttyAMA0,115200 \
        root=/dev/mmcblk0p2 \
        earlycon=pl011,mmio32,0x20201000" \
    -dtb bcm2708-rpi-zero-w.dtb
...
[    2.127829] bcm2835-wdt bcm2835-wdt: Broadcom BCM2835 watchdog timer
[    2.128367] 8<--- cut here ---
[    2.128451] Unhandled fault: external abort on non-linefetch (0x008) at 0xdc975020
[    2.128645] [dc975020] *pgd=17fdb841, *pte=2000a653, *ppte=2000a417
[    2.129201] Internal error: : 8 [#1] ARM
[    2.129409] Modules linked in:
[    2.129599] CPU: 0 PID: 16 Comm: kworker/u2:1 Not tainted 6.1.21+ #1642
[    2.129825] Hardware name: BCM2835
[    2.130058] Workqueue: events_unbound deferred_probe_work_func
[    2.130579] PC is at bcm2835_power_probe+0x64/0x294
[    2.130746] LR is at trace_hardirqs_on+0x38/0x118
[    2.130881] pc : [<c0560aa0>]    lr : [<c00f1db4>]    psr: a0000013
[    2.131040] sp : dc865c48  ip : 00000000  fp : c0d36654
[    2.131176] r10: c0d38498  r9 : 00000000  r8 : 00000001
[    2.131314] r7 : 00000000  r6 : c18f8020  r5 : 00000000  r4 : c18ecc20
[    2.131483] r3 : dc975000  r2 : 00000000  r1 : 00000000  r0 : c18f8020
[    2.131691] Flags: NzCv  IRQs on  FIQs on  Mode SVC_32  ISA ARM  Segment user
[    2.131884] Control: 00c5387d  Table: 00004008  DAC: 00000055
[    2.132053] Register r0 information: non-slab/vmalloc memory
[    2.132376] Register r1 information: NULL pointer
[    2.132528] Register r2 information: NULL pointer
[    2.132651] Register r3 information: 0-page vmalloc region starting at 0xdc975000 allocated at __devm_ioremap+0xa4/0xbc
[    2.132956] Register r4 information: slab kmalloc-64 start c18ecc00 pointer offset 32 size 64
[    2.133415] Register r5 information: NULL pointer
[    2.133548] Register r6 information: non-slab/vmalloc memory
[    2.133700] Register r7 information: NULL pointer
[    2.133822] Register r8 information: non-paged memory
[    2.133962] Register r9 information: NULL pointer
[    2.134084] Register r10 information: non-slab/vmalloc memory
[    2.134231] Register r11 information: non-slab/vmalloc memory
[    2.134376] Register r12 information: NULL pointer
[    2.134516] Process kworker/u2:1 (pid: 16, stack limit = 0x(ptrval))
[    2.134787] Stack: (0xdc865c48 to 0xdc866000)
[    2.134959] 5c40:                   c1220210 c1220200 00000001 c1220210 00000000 c0d31620
[    2.135164] 5c60: 00000000 00000001 00000000 c0d38498 c0d36654 c05b28b8 c1220210 00000000
[    2.135363] 5c80: c0d31620 00000000 00000001 c05b05f8 c1220210 c0d31620 c1220210 00000005
[    2.135563] 5ca0: 00000001 c05b086c c0e036c4 c0d31620 c1220210 c05b0904 00000001 c0d31620
[    2.135760] 5cc0: dc865d14 c1220210 00000001 c05b0ca0 00000000 dc865d14 c05b0c04 c0c2f02c
[    2.135960] 5ce0: 00000001 c05ae830 00000001 c117811c c12c3934 c68ecfcf 00000000 c1220210
[    2.136159] 5d00: c0c2f02c c1220254 c0c2f02c c05b0470 c18ecf40 c1220210 00000001 c68ecfcf
[    2.136358] 5d20: c1220210 c1220210 c0d36ae0 c0c2f02c 00000000 c05af598 c1220210 c11f4010
[    2.136556] 5d40: c0e03698 c05ac7f8 c1220210 c18ee080 c18ee080 c089ced0 c0c2f02c c68ecfcf
[    2.136755] 5d60: c1220200 c091ac70 00000000 c1220200 c1220210 00000000 c11f4010 00000000
[    2.136961] 5d80: 00000000 c05b2578 c091ac70 ffffffff c1220200 c091ac70 00000000 c11f4010
[    2.137160] 5da0: 00000000 c05d6f68 00000000 c0d368b4 c1008800 ffffffff 00000010 00000001
[    2.137360] 5dc0: c1220210 00000024 c11f4010 00000000 c05d6b60 c68ecfcf c091ac70 c11f4010
[    2.137559] 5de0: c18ecf20 ffffffff c091ac70 00000001 c101900d c0d368b4 c1008800 c05d72f0
[    2.137756] 5e00: 00000000 00000000 00000000 c18ecc20 c11f4000 c18ecc20 c11f4010 d7be19d8
[    2.137954] 5e20: 00000001 c05d5178 00000000 00000000 00000000 c11f4010 00000000 c11f4010
[    2.138152] 5e40: 00000000 c0d37f28 00000000 c05b28b8 c11f4010 00000000 c0d37f28 00000000
[    2.138351] 5e60: 00000001 c05b05f8 c11f4010 c0d37f28 c11f4010 00000004 00000001 c05b086c
[    2.138549] 5e80: c0e036c4 c0d37f28 c11f4010 c05b0904 00000001 c0d37f28 dc865eec c11f4010
[    2.138748] 5ea0: 00000001 c05b0ca0 00000000 dc865eec c05b0c04 c0c2f02c 00000001 c05ae830
[    2.138945] 5ec0: 00000001 c117811c c1834034 c68ecfcf c0d368b4 c11f4010 c0c2f02c c11f4054
[    2.139142] 5ee0: c0d3688c c05b0470 c05afa58 c11f4010 00000001 c68ecfcf c11f4010 c11f4010
[    2.139341] 5f00: c0d36ae0 c0d3688c 00000000 c05af598 c11f4010 c0d36880 c0d36880 c05afa78
[    2.139539] 5f20: c0d368b0 c1005f60 00000040 c1019000 00000000 c003c10c c1008818 c0ca14c0
[    2.139738] 5f40: c1005f60 c1008800 c1005f78 c1008818 c0ca14c0 00000088 c0d7ee77 c003c5d0
[    2.139937] 5f60: 60000013 00000000 00000040 c120b8e0 c1209c40 c003c394 c1005f60 dc839ec0
[    2.140136] 5f80: c1229040 00000000 00000000 c0042c84 c120b8e0 c0042bc4 00000000 00000000
[    2.140341] 5fa0: 00000000 00000000 00000000 c0008300 00000000 00000000 00000000 00000000
[    2.140541] 5fc0: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
[    2.140739] 5fe0: 00000000 00000000 00000000 00000000 00000013 00000000 00000000 00000000
[    2.141365]  bcm2835_power_probe from platform_probe+0x60/0xc0
[    2.141547]  platform_probe from really_probe+0xcc/0x2b8
[    2.141689]  really_probe from __driver_probe_device+0x88/0xec
[    2.141837]  __driver_probe_device from driver_probe_device+0x34/0xcc
[    2.141998]  driver_probe_device from __device_attach_driver+0x9c/0xcc
[    2.142163]  __device_attach_driver from bus_for_each_drv+0x84/0xcc
[    2.142327]  bus_for_each_drv from __device_attach+0xf4/0x1a0
[    2.142476]  __device_attach from bus_probe_device+0x8c/0x94
[    2.142620]  bus_probe_device from device_add+0x378/0x7b4
[    2.142761]  device_add from platform_device_add+0x108/0x20c
[    2.142907]  platform_device_add from mfd_add_devices+0x2cc/0x5e4
[    2.143067]  mfd_add_devices from devm_mfd_add_devices+0x70/0xb8
[    2.143221]  devm_mfd_add_devices from bcm2835_pm_probe+0x130/0x1ac
[    2.143380]  bcm2835_pm_probe from platform_probe+0x60/0xc0
[    2.143530]  platform_probe from really_probe+0xcc/0x2b8
[    2.143670]  really_probe from __driver_probe_device+0x88/0xec
[    2.143817]  __driver_probe_device from driver_probe_device+0x34/0xcc
[    2.143979]  driver_probe_device from __device_attach_driver+0x9c/0xcc
[    2.144141]  __device_attach_driver from bus_for_each_drv+0x84/0xcc
[    2.144298]  bus_for_each_drv from __device_attach+0xf4/0x1a0
[    2.144445]  __device_attach from bus_probe_device+0x8c/0x94
[    2.144589]  bus_probe_device from deferred_probe_work_func+0x80/0xac
[    2.144752]  deferred_probe_work_func from process_one_work+0x204/0x48c
[    2.144925]  process_one_work from worker_thread+0x23c/0x53c
[    2.145071]  worker_thread from kthread+0xc0/0xe4
[    2.145197]  kthread from ret_from_fork+0x14/0x34
[    2.145344] Exception stack(0xdc865fb0 to 0xdc865ff8)
[    2.145474] 5fa0:                                     00000000 00000000 00000000 00000000
[    2.145675] 5fc0: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
[    2.145871] 5fe0: 00000000 00000000 00000000 00000000 00000013 00000000
[    2.146158] Code: e5943008 e5863008 e594200c e586200c (e5933020) 
[    2.146474] ---[ end trace 0000000000000000 ]---
[    2.146660] note: kworker/u2:1[16] exited with irqs disabled
```

- [The kernel's command-line parameters][cmdline]

```sh
$ qemu-system-aarch64 -machine raspi0 \
    -sd 2024-10-22-raspios-bullseye-armhf.img \
    -nographic \
    -kernel kernel.img \
    -append "console=ttyAMA0,115200 \
        root=/dev/mmcblk0p2 \
        earlycon=pl011,mmio32,0x20201000 \
        initcall_blacklist=bcm2835_pm_driver_init" \
    -dtb bcm2708-rpi-zero-w.dtb
...
[    2.589029] mmcblk0: mmc0:cda9 QEMU! 8.00 GiB 
[    2.597301] /dev/root: Can't open blockdev
[    2.597579] VFS: Cannot open root device "mmcblk0p2" or unknown-block(0,0): error -6
[    2.597774] Please append a correct "root=" boot option; here are the available partitions:
[    2.598125] 0100            4096 ram0 
[    2.598226]  (driver?)
[    2.598421] 0101            4096 ram1 
[    2.598436]  (driver?)
[    2.598600] 0102            4096 ram2 
[    2.598617]  (driver?)
[    2.598784] 0103            4096 ram3 
[    2.598800]  (driver?)
[    2.598968] 0104            4096 ram4 
[    2.598984]  (driver?)
[    2.599158] 0105            4096 ram5 
[    2.599174]  (driver?)
[    2.599343] 0106            4096 ram6 
[    2.599359]  (driver?)
[    2.599533] 0107            4096 ram7 
[    2.599546]  (driver?)
[    2.599698] 0108            4096 ram8 
[    2.599710]  (driver?)
[    2.599862] 0109            4096 ram9 
[    2.599874]  (driver?)
[    2.600040] 010a            4096 ram10 
[    2.600054]  (driver?)
[    2.600209] 010b            4096 ram11 
[    2.600221]  (driver?)
[    2.600376] 010c            4096 ram12 
[    2.600389]  (driver?)
[    2.600543] 010d            4096 ram13 
[    2.600555]  (driver?)
[    2.600709] 010e            4096 ram14 
[    2.600722]  (driver?)
[    2.600877] 010f            4096 ram15 
[    2.600890]  (driver?)
[    2.601057] b300         8388608 mmcblk0 
[    2.601118]  driver: mmcblk
[    2.601468] Kernel panic - not syncing: VFS: Unable to mount root fs on unknown-block(0,0)
[    2.601798] CPU: 0 PID: 1 Comm: swapper Not tainted 6.1.21+ #1642
[    2.602037] Hardware name: BCM2835
[    2.602703]  unwind_backtrace from show_stack+0x18/0x1c
[    2.603074]  show_stack from dump_stack_lvl+0x34/0x58
[    2.603228]  dump_stack_lvl from panic+0x108/0x314
[    2.603428]  panic from mount_block_root+0x164/0x250
[    2.603621]  mount_block_root from mount_root+0x208/0x250
[    2.603767]  mount_root from prepare_namespace+0x138/0x194
[    2.603909]  prepare_namespace from kernel_init_freeable+0x1e4/0x228
[    2.604071]  kernel_init_freeable from kernel_init+0x1c/0x11c
[    2.604218]  kernel_init from ret_from_fork+0x14/0x34
[    2.604411] Exception stack(0xdc821fb0 to 0xdc821ff8)
[    2.604701] 1fa0:                                     00000000 00000000 00000000 00000000
[    2.604906] 1fc0: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
[    2.605112] 1fe0: 00000000 00000000 00000000 00000000 00000013 00000000
[    2.605714] ---[ end Kernel panic - not syncing: VFS: Unable to mount root fs on unknown-block(0,0) ]---
```

```sh
$ qemu-system-aarch64 -machine raspi0 \
    -sd 2024-10-22-raspios-bullseye-armhf.img \
    -nographic \
    -kernel kernel.img \
    -append "console=ttyAMA0,115200 \
        root=/dev/mmcblk0p2 \
        earlycon=pl011,mmio32,0x20201000 \
        initcall_blacklist=bcm2835_pm_driver_init \
        rootwait" \
    -dtb bcm2708-rpi-zero-w.dtb
...
Raspbian GNU/Linux 11 raspberrypi ttyAMA0

raspberrypi login: pi
Password:
Linux raspberrypi 6.1.21+ #1642 Mon Apr  3 17:19:14 BST 2023 armv6l

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
pi@raspberrypi:~$ ls
Bookshelf  Documents  Music     Public     Videos
Desktop    Downloads  Pictures  Templates
pi@raspberrypi:~$ touch test
touch: cannot touch 'test': Read-only file system
pi@raspberrypi:~$
```

```sh
$ qemu-system-aarch64 -machine raspi0 \
    -sd 2024-10-22-raspios-bullseye-armhf.img \
    -nographic \
    -kernel kernel.img \
    -append "console=ttyAMA0,115200 \
        root=/dev/mmcblk0p2 \
        earlycon=pl011,mmio32,0x20201000 \
        initcall_blacklist=bcm2835_pm_driver_init \
        rootwait \
        rw" \
    -dtb bcm2708-rpi-zero-w.dtb
...
Raspbian GNU/Linux 11 raspberrypi ttyAMA0

raspberrypi login: pi
Password:
Linux raspberrypi 6.1.21+ #1642 Mon Apr  3 17:19:14 BST 2023 armv6l

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Tue Oct 22 14:17:28 BST 2024 on tty1
pi@raspberrypi:~$ ls
Bookshelf  Documents  Music     Public     Videos
Desktop    Downloads  Pictures  Templates
pi@raspberrypi:~$ touch test
pi@raspberrypi:~$
```

## Reference

- [Raspberry Pi operating system images][raspios]

- [Raspberry Pi Docs > Computer > Configuration][raspi conf]

- [mount(8)][mount]

- [losetup(8)][losetup]

- [QEMU Docs > System Emulation > QEMU System Emulator Targets > Arm System emulator][arm emul]

- [QEMU Docs > System Emulation > Invocation][invoc]

- [The kernel's command-line parameters][cmdline]

[raspios]: https://www.raspberrypi.com/software/operating-systems/

[raspi conf]: https://github.com/rewls/raspberry-pi-docs/blob/main/computers/configuration.md

[mount]: https://github.com/rewls/system-reference-manual/blob/main/mount-8.md

[losetup]: https://github.com/rewls/system-reference-manual/blob/main/losetup-8.md

[arm emul]: https://github.com/rewls/qemu-docs/blob/main/system-emulation/qemu-system-emulator-targets/arm-system-emulator.md

[invoc]: https://github.com/rewls/qemu-docs/blob/main/system-emulation/invocation.md

[cmdline]: https://github.com/rewls/the-linux-kernel-documentation/blob/main/administration/the-kernels-command-line-parameters.md
