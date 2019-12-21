# Monitoring

## Install  os from opendlv os script using bash file

### To get a Internet
After booting into a live disk archlinux: To get internet conenction: use wifi-menu
```bash
wifi-menu
```
Things to be changed in the script:


**Step1**:  Get network interface name, replace the network interface in the setup script.\
```
ip a
```
**Step2**: Change the network interface name\
**Step3**: 
```bash
#Append 
dialog wpa_supplicant 
#to the install_conf.sh
line software="base-devel gnu-netcat vim ifplugd wget openssh bash-completion screen"
```
## Afrer installation
### Install NVIDIA driver
```bash
# Install normal Nvidia driver
sudo pacman -S nvidia
# Install Nvidia driver 435.xx
sudo pacman -Ss nvidia
#Install the nvidia-dkms package if use custom kernel
sudo pacman -S nvidia-dkms
```
GeForce 20 series cards works with 418.xx, 430.xx and 435.xx Nvidia drivers GeForce 600/700/800/900/10 series cards works with 390.xx, 418.xx, 430.xx and 435.

### Install NVIDIA docker
```bash
git clone https://aur.archlinux.org/pakku.git
cd pakku
makepkg -si
pakku -S nvidia-docker
```
### Other tools

#### Install CAN utils
```bash
git clone https://github.com/linux-can/can-utils.git
cd can-utils
./autogen.sh
./configure
make
make install (with root privileges)
```
#### Gnome desktop
??????
#### VNC server
VNC : https://wiki.archlinux.org/index.php/TigerVNC
to run the vnc server:
```
vncserver :4 -depth 24 -geometry 1920x1080 -nolisten tcp
```
## Some useful notes / troule shooting
### PCIE Problem
If there is error message in $ dmesg from PCIE (peak CAN device)
```
sudo nano /etc/default/grub
```
find GRUB_CMDLINE_LINUX_DEFAULT=\
append pci=noaer
```
GRUB_CMDLINE_LINUX_DEFAULT=pci=noaer
```
save
```
grub-mkconfig -o /boot/grub/grub.cfg
```
### Change the boot order
In case you need to change the boot order

https://askubuntu.com/questions/216398/set-older-kernel-as-default-grub-entry

### Permissions
In case you need to add cfsd as sudoer

download https://aur.archlinux.org/cgit/aur.git/snapshot/linux-rt.tar.gz
```bash
tar -xzf tarfile

cd folder

makepkg -si --skippgpcheck

specify user pass

grub-mkconfig -o /boot/grub/grub.cfg
```