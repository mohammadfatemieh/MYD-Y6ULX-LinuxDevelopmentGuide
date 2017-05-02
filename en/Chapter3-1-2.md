# 3.1.2 Compiling U-Boot

Enter Bootloader directory, extract U-boot source tar ball:

    cd $DEV_ROOT/Bootloader
    tar -xvjf u-boot-2016.03.tar.bz2
    cd u-boot-2016.03

Compiling：

    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- distclean 
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- <config>
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf-

The <config> option value means different boot mode. The MYD-JA5D2X supports two boot modes.

Boot Mode | Config file
-------- | --------
NAND Flash | myd_ja5d2x_nandflash_defconfig
SPI Flash | myd_ja5d2x_spiflash_defconfig