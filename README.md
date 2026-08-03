# Overview
MTD dump of Dasan H660RM GPON ONT
>[!NOTE]
>You can find the dump within [Releases Tab](https://github.com/ButterWatt/H660RM-Dump/releases), unfortunately I couldn't get older version that contains CVE vulnerabilities (version 1.03-0022).
>
>Also MTD4 is `tclinux` version 1.03-0032, MTD7 is `tclinux` version 1.07-0019. Maybe U-boot will try to boot newer firmware, *I guess*

# License
This repository is licensed under GNU General Public License version 3 (GNU GPLv3), take a look at [GNU Website](https://www.gnu.org/licenses/gpl-3.0.html) or this [repo's license](https://github.com/ButterWatt/H660RM-Dump/blob/main/LICENSE). *I don't think that you will spend time for a license that longer than your tax invoice*


# Partition Table
    PARTITION |  SIZE    | ERASESIZE | DEFINITION     |                                            PARTITION INFO

      mtd0      00040000   00020000    bootloader       LZMA, P: 0x5D, D: 8388608, U: 199536, H: 0x10000

      mtd1      00040000   00020000    romfile          N/A
  
      mtd2      001431e5   00020000    kernel           LZMA, P: 0x5D, D: 8388608, U: 4099072, H:0x100 / JBOOT STAG, A: 4, T: 0x19A8DDB6
                                                        image S: 3603229812, image C: 0x837A, header C: 0xB96, H: 0x125304

      mtd3      00ed0000   00020000    rootfs           Squashfs LZMA, LE, version 4.0, I: 1157, B: 131072, T: 2017-12-15 12:51:17

      mtd4      02a00000   00020000    tclinux          LZMA, P: 0x5D, D: 8388608, U: 4099072, H: 0x100 / JBOOT STAG, A: 4, T: 0x19A8DDB6
                                                        image S: 3603229812, image C: 0x837A, header C: 0xB96, H: 0x125304 / Squashfs
                                                        LZMA, LE, version 4.0, S: 15504546, I: 1157, B: 131072, T: 2017-12-15 12:51:17
                                                        H: 0x1431E5

      mtd5      00144199   00020000    kernel_slave     LZMA, P: 0x5D D:8388608, U: 4164608, H: 0x100

      mtd6      00f80000   00020000    rootfs_slave     Squashfs LZMA, LE, version 4.0, S: 16222021, I: 1101, B: 131072
                                                        T: 2018-04-23 12:32:12
    
      mtd7      02a00000   00020000    tclinux_slave    LZMA, P: 0x5D, D: 8388608, U: 4164608, H: 0x100 / Squashfs filesystem, LE
                                                        version 4.0, S: 16222021, I: 1101, B:131072, H: 0x144199
      
      mtd8      00020000   00020000    license_ctrl     N/A
    
      mtd9      00100000   00020000    license          N/A
    
      mtd10     00100000   00020000    license2         N/A
    
      mtd11     00500000   00020000    user_rootfs      JFFS2, BE
    
      mtd12     00040000   00020000    wlan_cal         N/A
    
      mtd13     000a0000   00020000    reservearea      N/A
    
    P: PROPERTIES | D: DICTIONARY SIZE (byte) | U: UNCOMPRESSED (byte) | S: SIZE (byte) | B: BLOCKSIZE (byte) | I: INODE
    
    H: HEXDECIMAL | A: IMAGE ID | T: TIMESTAMP | C: CHECKSUM | LE: LITTLE ENDIAN | BE: BIG ENDIAN
# NAND Table
    START ADDRESS    |     END ADDRESS   |    PARTITION NAME
      0x00000000           0x00040000         bootloader
      0x00040000           0x00080000         romfile
      0x00080000           0x001c31e5         kernel
      0x001c31e5           0x010931e5         rootfs
      0x00080000           0x02a80000         tclinux
      0x02a80000           0x02bc31e5         kernel_slave
      0x02bc31e5           0x03a931e5         rootfs_slave
      0x02a80000           0x05480000         tclinux_slave
      0x05480000           0x054a0000         license_ctrl
      0x054a0000           0x055a0000         license
      0x055a0000           0x056a0000         license2
      0x056a0000           0x05ba0000         user_rootfs
      0x07500000           0x07540000         wlan_cal
      0x07540000           0x075e0000         reservearea
# Device Information
Device Model: `H660RM`

Storage Chip: `Macronix MXIC MX35LF1GE4AB-Z4I SPI NAND 128MB 1Gbit`

Memory Chip: `Winbond W631GG6KB-12 128MB DDR3 64M*16-bit 1Gbit`

SoC: `EcoNet EN751221`

WiFi: `Mediatek MT7615DN`

Landline Chip: `Microchip LE9642PQC`

GPON: `HiSense LTY9775M-CHG2`

Default telnet/UART credentials: `admin:vertex25ektks123`

*Special Name*: `Dasucks`
# Device's U-boot available commands
    ?                                   Print out help messages.
    help                                Print out help messages.
    go                                  Booting the linux kernel.
    decomp                              Decompress kernel image to ram.
    memrl <addr>                        Read a word from addr.
    memwl <addr> <value>                Write a word to addr.
    dump <addr> <len>                   Dump memory content.
    jump <addr>                         Jump to addr.
    flash <dst> <src> <len> <oob>       Write to flash from src to dst(oob: write nand oob if 1).
    imginfo                             Show images info.
    bootcfginfo                         Show Bootconfig info.
    modelname <<Model Name>             Set Model Name.
    swcompatibility <STRING>            Set S/W Compatibility.
    partnumber <STRING>                 Set Device Part Number.
    SN <SN>                             Set SN([1-17]length)
    onutype <value>                     Set ONU type
    statevalue <value>                  Set New State Value.
    ethaddr <value>                     Set New Eth Address.
    flashrd <offset> <length>           Read NAND data.
    flashersec <offset> <length         Erase flash sectors containing given region.
    bdstore <flash dst> <bin src>       Do backdoor config store
    bdshow                              Show backdoor config
    bdswitch[1|0]                       Enable or disable backdoor function
    ddrcalswitch[1|0]                   Enable or disable ddr calibration funciton
    drambistswitch[0|1|2]               disable or enable, and quick or normal test
    xmdm <addr> <len>                   Xmodem receive to addr.
    miir <phyaddr> <reg>                Read ethernet phy reg.
    miiw <phyaddr> <reg> <value>        Write ethernet phy reg.
    cpufreq <freq num> / <m> <n>        Set CPU Freq <156~450>(freq has to be multiple of 6)
    ipaddr <ip addr>                    Change modem's IP.
    httpd                               Start Web Server
    ddrdrv <..>                         Change DDR driving length
    mtd                                 Print NAND partition start/end addresses
>[!IMPORTANT]
> Do not touch any critical commands like `cpufreq`, `flashersec` or `flash` if you are NOT CERTAIN what you're about to do. (Make sure you have a programmer to reflash if something goes wrong while using critical commands)
# Checksum
H660RM Dump version 1.7: `sha256:07acc61526579f51c1dcdd8818658c5e652f56f5c2bd7fdc5cc143c4adbe9d70`
