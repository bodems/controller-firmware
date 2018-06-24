# controller-firmware
Generate OpenWRT based controller firmwares for a RaspberryPi

## About this project
The goal of this project is to develop a firmware for embedded devices based on OpenWRT, suited for charging controllers for electric vehicles following the IEC 61851 standard.
As security is very important, updating the system should be as easy as possible. This will be possible via a webinterface. Config files are preserved.

## Building the firmware on a debian based system

```bash
    sudo apt install subversion g++ zlib1g-dev build-essential git python
    sudo apt install libncurses5-dev gawk gettext unzip file libssl-dev wget
```
Build commands for the console:
```bash
    git clone https://git.openwrt.org/openwrt/openwrt.git
    cd openwrt
    git checkout tags/v17.01.4
    
    git clone https://github.com/bodems/controller-firmware.git
    cp -rf controller-firmware/files controller-firmware/package controller-firmware/feeds.conf .
    
    ./scripts/feeds update -a
    ./scripts/feeds install -a
    
    rm -rf firmware tmp
    
    make menuconfig
```
Now select the right "Target System" and "Target Profile" for your embedded controller:

For example, for the Raspberry Pi 3, select:
* `Target System => Broadcom BCM27xx
* `Subtarget => BCM2710 64 bit based boards
* `Target Profile => Raspberry Pi 3B/3B+

Now start the build process. This takes some time:
```bash
    make
```
* You have the opportunity to compile the firmware on more CPU Threads. 
E.g. for 4 threads type* `make -j4` .


The **firmware image** files can now be found under the `bin/targets` folder. Use the firmware update functionality of your router and upload the factory image file to flash it with the controller firmware. The sysupgrade images are for updates.


## Credits
This is highly inspired by https://github.com/freifunk-bielefeld/firmware and some parts (e.g. the webinterface) is reused.
