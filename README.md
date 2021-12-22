![OpenWrt logo](include/logo.png) 

openwrt-archerc5
================

>Note: `This is a development fork of OpenWRT. Resolving a specific SoC Router. Uf you're ere for that, I wish you the best. I take no responsibilty if you mess up. I will uplaod completed firmware releases shortly as well as video.

A Fork of OpenWRT with TP-Link Archer C5v4 Support

Credit and Respect to Serge Vasilugin who created the patch that made
this possible. His GitHub: https://github.com/ggbruno

Due to the Realtek RTL8367S SoC, OpenWRT has deemed this router
unsupported. If you follow the instructions, you will be able to install
custom firmware up to current Version 21.02.

For the environment I use. Prerequisites:

OS: GNU/Linux and Unix like distribution. I used Ubuntu Server 20.04
under a VM environment.

THIS PART PEOPLE JUST DONT SEEM TO GET:

1.  An account that is NON-Root. I.E. A standard account.
2.  The following packages:


```sh
sudo apt update 
sudo apt install -y build-essential ccache ecj fastjar \
file g++ gawk gettext git java-propose-classpath libelf-dev libncurses5-dev \
libncursesw5-dev libssl-dev python python2.7-dev python3 unzip wget \
python3-distutils python3-setuptools python3-dev rsync subversion \
swig time xsltproc zlib1g-dev
```

The above is what OpenWRT recommned. Its the base build tools. But YOU DO NEED the rest. So Step but step. 
```sh
sudo apt -y install subversion mercurial
```


```sh
sudo apt -y install asciidoc bash binutils bzip2 flex git-core g++ gcc \
util-linux  gawk help2man intltool libelf-dev zlib1g-dev make \
libncurses5-dev libssl-dev patch perl-modules python2-dev python3-dev \
unzip wget gettext xsltproc zlib1g-dev
```

> Note: `I may have duplicated packaes by mistake. They Simply wont install again.''

```sh
sudo apt -y install libboost-dev libxml-parser-perl libusb-dev bin86 bcc \
sharutils gcc-multilib openjdk-8-jdk
```

> Note: `openjdk-7-jdk is no longer available on Ubuntu 20.04. The release
is as per above.'' 

3.  You need to go to /home and type sudo mkdir \~/openwrt (OpenWRT
    support calls this the root folder. A kinda conflicts with the fact
    that all compiling must NOT be root)
4.  fomr home type ls -sl. The folder is root:root permission now. You
    need to type: sudo chown {non-sudo user}:{non-sudo group}
5.  Now enter \~/openwrt as your non-sudo user. From this point,
    everything must be done as a non-sudo
6.  type git clone https://github.com/openwrt/openwrt.git
7.  Once cloned, Select Master by typing: git branch -a; then git switch
    master
8.  You can type git pull to see if any new patches or updates have
    changed
9.  Now you should be in v21.02
10. ./scripts/feeds update -a
11. ./scripts/feeds install -a
12. wget
    https://patch-diff.githubusercontent.com/raw/openwrt/openwrt/pull/4327.patch
    (This is the realtek patch that will add the Archer c5v4 in
    menuconfig)
13. git apply 4327.patch (if you have no errors or issues here, you
    should be smooth sailing)
14. make defconfig
15. make menuconfig Inside the menuconfig: set Target System: MediaTek
    Ralink MIPS set Subtarget: MT7620.. set Target Profile: TP-Link
    Archer C5 v4

There's a lot of customising here. I would suggest starting with just
the above, and if you prefer WebUI, add Luci.

16. Save
17. make -j{see notes} download (-j4 is 4 cores; if you have issues try
    make -j2 or make -j1 - the download parameter will speed up
    compiling)
18. make -j4 V=s (This is 4 core CPU with verbose so you can see the
    compilation)

Now sit back, have a few cups of coffee. The compilation takes a while,
and uses about 20-30 gig.

Good luck!


![2560px-TPLINK_Logo_2 svg](https://user-images.githubusercontent.com/2247180/147079098-268bb575-6389-4832-82fc-318684879cf4.png)
