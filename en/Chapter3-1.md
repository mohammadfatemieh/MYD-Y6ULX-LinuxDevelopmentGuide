# 3.1 Compiling U-Boot

Enter Bootloader directory, extract U-boot source tar ball:

```
cd $DEV_ROOT/Bootloader
tar -xvjf u-boot-2016.03.tar.bz2
cd u-boot-2016.03
```

Compiling：
 
```
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- distclean 
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- <config>
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf-
```

The <config> option value is different boot mode. The MYS-6ULX supports four boot modes.

Boot Mode | Config file
-------- | --------
MYS-6UL-IND NAND Flash | mys_imx6ul_14x14_nand_defconfig
MYS-6UL-IND eMMC Flash | mys_imx6ul_14x14_emmc_defconfig
MYS-6ULL-IoT NAND Flash | mys_imx6ull_14x14_nand_defconfig
MYS-6ULL-IoT eMMC Flash | mys_imx6ull_14x14_emmc_defconfig

U-Boot will search and execute a script file "boot.scr" when U-Boot booting up. It used to change boot type in temporary.Next is use "mys-imx6ul-boot-sdcard.txt" to generate the "boot.scr" file as example. The mkimage tool source code is locate in "U-Boot/tools" directory. It will be compile after U-Boot compiled.

```
cat mys-imx6ul-boot-sdcard.txt
setenv mmcroot '/dev/mmcblk0p2 rootwait rw rootdelay=5 mem=256M'
setenv mmcargs 'setenv bootargs console=${console},${baudrate} root=${mmcroot} mtdparts=gpmi-nand:5m(boot),10m(kernel),1m(dtb),-(rootfs)'
run mmcargs
fatload mmc 0 0x83000000 zImage
fatload mmc 0 0x84000000 mys-imx6ul-14x14-evk-emmc.dtb
bootz 0x83000000 - 0x84000000

./tool/mkimage -A arm -T script -O linux -d mys-imx6ul-boot-sdcard.txt boot.scr
```