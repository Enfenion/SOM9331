Warning: These instructions are not well-tested, and should not be trusted.

# Compilation instructions

Patched code from: https://github.com/10to7/SOM9331

First, install dependencies (not exhaustive):

    sudo apt-get install git wget make build-essential patch gawk libncurses5-dev

Clone Barrier Breaker repo:

    git clone -b barrier_breaker git://github.com/openwrt/archive.git openwrt
    cd openwrt

Download linux kernel to dl-dir (old mirror outdated):

    Either download only the libs you need:

    mkdir dl
    wget -O dl/linux-3.10.49.tar.xz https://github.com/jslink/openwrt-trunk-dl/blob/master/linux-3.10.49.tar.xz?raw=true
    wget -O dl/libubox-2014-08-04-dffbc09baf71b294185a36048166d00066d433b5.tar.gz https://github.com/jslink/openwrt-trunk-dl/blob/master/libubox-2014-08-04-dffbc09baf71b294185a36048166d00066d433b5.tar.gz?raw=true
    wget -O dl/util-linux-2.24.1.tar.xz "https://github.com/jslink/openwrt-trunk-dl/blob/master/util-linux-2.24.1.tar.xz?raw=true"
    wget -O dl/netifd-2014-09-08.1-46c569989f984226916fec28dd8ef152a664043e.tar.gz "https://repo.turris.cz/downloads/netifd-2014-09-08.1-46c569989f984226916fec28dd8ef152a664043e.tar.gz"

    Or clone the whole repository and download the one missing file:

    git clone https://github.com/jslink/openwrt-trunk-dl dl
    wget -O dl/netifd-2014-09-08.1-46c569989f984226916fec28dd8ef152a664043e.tar.gz "https://repo.turris.cz/downloads/netifd-2014-09-08.1-46c569989f984226916fec28dd8ef152a664043e.tar.gz"


Patch in SOM9331:

    git clone https://github.com/Enfenion/SOM9331.git
    patch -p0 < SOM9331/som9331.patch

Update packages:

    ./scripts/feeds update -a && ./scripts/feeds install -a

Select correct targets:
  Target System (Atheros AR7xxx/AR9xxx)
  Target Profile, OpenEmbed SOM9331, listed after TP-Link
  LiCL - Collections - luci (select with * to compile it into the image)
         Translations - luci-i8n-english

    make defconfig
    make menuconfig

Compile, and wait (although buildroot doesn't like -jX OpenWRT doesn't seem to care):

    make -j8 V=s

Or alternatively:

    export BR2_JLEVEL=8
    make V=s

Install "bin/ar71xx/openwrt-ar71xx-generic-som9331-squashfs-sysupgrade.bin" using the web interface.
