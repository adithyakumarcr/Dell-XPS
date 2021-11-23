# Dell-XPS Installation guide for Ubuntu 18.04LTS
 
### Installation Procedure for Dell XPS 15 9510 

1) Fix touch pad right click button

```
gsettings set org.gnome.desktop.peripherals.touchpad click-method areas
````

2) Disable Safe Boot from BIOS Setup
3) Install Nvidia v4.70.63.01 Drivers
4) Download mainlines to update kernel.
```
sudo add-apt-repository ppa:cappelikan/ppa
sudo apt update
sudo apt install mainline
```
5) Select Kernel v5.11.0
6) If you have upgraded your kernel, then the latest kernel should load. If you have downgraded then. While boot select the advanced options and select this version. 
7) By default, the brightness control should work now. The nvidia drivers should work all fine. Wifi/BT will not work now. 
8) To fix this connect to internet via Ethernet or reboot to Wifi working kernel. 
9) Update source files and upgrade
```
sudo apt-get update
sudo apt-get dist-upgrade -y
```
10) Download the Latest Git and Build-Essential packages
```
sudo apt-get install -y git
sudo apt-get install -y build-essential
```
11. Download the Iwlwifi-Firmware.git repository
```
git clone git://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git
cd linux-firmware
sudo cp iwlwifi-* /lib/firmware/
cd ..
git clone https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git
```
12. If you are on old Kernel, reboot to the new one(v5.11.0)

```
cd backport-iwlwifi
sudo make defconfig-iwlwifi-public
sudo make -j4
sudo make install
update-initramfs -u
sudo reboot now
```

Tested with Ubuntu 18.04LTS. Graphic card works and all the other peripherals work normally. 

If you had installed other kernels. Dont forget to remove them. It can be easily removed via Mainlines. 



