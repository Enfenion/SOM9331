Warning: These instructions are not tested, and should not be trusted or used by anyone.

# Compilation instructions

Patched code from: https://github.com/10to7/SOM9331

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

    clone https://github.com/jslink/openwrt-trunk-dl dl
    wget -O dl/netifd-2014-09-08.1-46c569989f984226916fec28dd8ef152a664043e.tar.gz "https://repo.turris.cz/downloads/netifd-2014-09-08.1-46c569989f984226916fec28dd8ef152a664043e.tar.gz"


Patch in SOM9331:

    clone https://github.com/Enfenion/SOM9331.git
    patch -p0 < SOM9331/som9331.patch

Update packages:

    ./scripts/feeds update -a && ./scripts/feeds install -a

Select correct target:  (Target System (Atheros AR7xxx/AR9xxx), Target Profile (OpenEmbed SOM9331) after TP-Link)

    make defconfig
    make menuconfig

Compile:

    make -j8 V=s

