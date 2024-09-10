# M5Pi
![](https://github.com/imliubo/M5Pi/blob/main/assets/images/M5Pi-02.jpg)
M5Pi is an open source Linux embedded development board, using Allwinner F1C200s CPU, and has a beautiful shell.

## Try to use a pre-compiled system image
```shell
wget https://github.com/imliubo/M5Pi/releases/download/v0.1-alpha/M5Pi-sysimage-sdcard-v0.1-alpha.tar.gz
tar -zxvf M5Pi-sysimage-sdcard-v0.1-alpha.tar.gz
dd if=sysimage-sdcard.img of=/dev/sdX  # Please make sure "X" is your TF card mount point.
```

## Try to compile your custom system image

### Install
```shell
sudo apt install wget unzip build-essential git bc swig libncurses-dev libpython3-dev libssl-dev
sudo apt install python3-distutils
```

### Build
```shell
git clone --recursive https://github.com/imliubo/M5Pi
cd M5Pi/buildroot-M5Pi
make IAMLIUBO_m5pi_defconfig  # Use the default config.
make -j ${YOUR_CPU_COUNT}
```

### Build with custom config
```shell
make menuconfig
make uboot-menuconfig
make linux-menuconfig
```

### Flash
```shell
dd if=buildroot-M5Pi/output/images/sysimage-sdcard.img of=/dev/sdX  # Please make sure "X" is your TF card mount point.
```

## License
1. Hardware: CC BY-NC-SA 4.0
2. buildroot-M5Pi: follow the upstream

## Links
[【自 制】这 可 能 是 最 精 致 的 Pi 了【Linux 小主机 | 开 源 | 硬 核】](https://www.bilibili.com/video/BV1RV411W7eH/)

[[开源项目-记录贴]扔掉你手中的开发板，跟我来自制基于F1C100s/F1C200s的M5Pi吧!](https://whycan.com/t_6402.html)

[How-to-make-a-M5Pi](./Tutorials/How-to-make-a-M5Pi.md)

## Thanks to the sponsor Seeed!
Seeed Fusion PCB Assembly Service offers one-stop prototyping for PCB manufacture, PCB assembly and as a result they produce superior quality PCBs and Fast Turnkey PCBA from 7 working days. When you prototype with Seeed Fusion, they can definitely provide Free DFA and Free functional tests for you! Check out their website to know more: https://www.seeedstudio.com/prototype-pcb-assembly.html
