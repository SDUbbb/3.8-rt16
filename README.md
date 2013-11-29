kernel
======

Kernel for the beagleboard.org boards

This is a known working 3.8.13-rt16 kernel patchset for beaglebone black boards.

The patchset was original downloaded from github.com/beagleboard/kernel 

The patch.sh was edited and a 3.8.13-rt16 patch from https://www.kernel.org/pub/linux/kernel/projects/rt/
is used during the patching.

Stephan Klann, University of Southern Denmark, stkla10@student.sdu.dk

usage
======

./patch.sh

To fix and build it:

```
cd kernel
cp ../configs/.config .config
cp ../base.c drivers/of/base.c
cp ../am335x-pm-firmware.bin firmware/am335x-pm-firmware.bin
make ARCH=arm CROSS_COMPILE=arm-xxxx-linux-gnueabi- uImage dtbs
```
...
cd arch/arm/boot
...

copy over uImage

...
cd dts/
...

and am335x-boneblack.dtb to /boot

Change uEnv.txt on the BEAGLE_BONE partition

```
devtree=/boot/am335x-boneblack.dtb
dtboot=run mmcargs; ext2load mmc ${mmcdev}:2 ${kloadaddr} ${bootfile} ; ext2load mmc ${mmcdev}:2 ${fdtaddr} ${devtree} ; bootm ${kloadaddr} - ${fdtaddr}
uenvcmd=run dtboot
optargs=consoleblank=0
```
