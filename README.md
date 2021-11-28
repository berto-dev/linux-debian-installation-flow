

![Debian](./resources/banner.png)

------



## LINUX DEBIAN - CUSTOM START PIPELINE

A pipelines it's a simple step by step roles for make somethings better.
This file is a simple annotations for custom installation of linux and relative desktop environment based on *debian + gnome + configuration and extras*.

Important note: **it's under costruction and based on personal use.** 



------



## Installation:



##### - download and mod iso images

download an non-free iso:  https://www.debian.org/CD/http-ftp/#firmware<br>

// *for me:*<br>
// https://cdimage.debian.org/debian-cd/11.1.0/amd64/iso-dvd/*<br>
// [firmwarepack.zip](.\resources\firmwarepack.zip) *you can and copy n paste all firmaware in new iso inside firmaware/deb11*<br>



##### -  flash , mod n burn an iso you can use:

 - https://anyburn.com/ (mod/burn) 
 - https://www.balena.io/etcher/ (flashing)
 - https://rufus.ie/it/ (burn)


for easy way to mod an iso: 

https://www.zipware.org/

###### - helps

maked iso follow graphical install instruction:
https://www.debian.org/releases/bullseye/installmanual
a youtube simple tutorial/preview
https://www.youtube.com/watch?v=nR-Ux2znypg





### after install:

------



##### - Resolve/Set sudoers "super user do"

in terminal: 
- get in root	
	**::** `su root`
- install sudo
	**::** ` apt-get install sudo -y`<br>
- add your username
	**::** ` sudo adduser USERNAME sudo`<br>
	-open root permission
	**::** `sudo chmod  0440  /etc/sudoers`<br>
	**::** `sudo reboot`<br>

##### - if wont, now you can change your hostname

**::**  `sudo gedit /etc/hostname`<br>
**::**  `sudo gedit /etc/hosts`<br>
**::**  `sudo reboot`<br>

##### -  update all:

**::**  `sudo apt-get update`<br>
**::**  `sudo apt-get upgrade`<br>
**::**  `sudo apt-get dist-upgrade `<br>

##### - remove cd/rom from depencies update and commands

**::**  `sudo sed -i '/cdrom/d' /etc/apt/sources.list`<br>
**::**  `grep -v '#' /etc/apt/sources.list`<br>

##### - Install Git Commands

**::**  `sudo apt update`<br>
**::**  `sudo apt-get install build-essential dkms git`<br>

##### - Install USB RTL8812BU Chipset Wifi

a - you can find drivere here: https://github.com/morrownr/88x2bu<br>
b - open terminal and enter into forlder of file (try drag folder)<br>
**::**  `sudo ./install-driver.sh`<br>

##### - add windows (or other) to grub

	a - :: sudo blkid and get UEFI WINDOW UIDD CODE
	b - Install and Open GrubCustomizer:
		Select "Chainloader",
		write a Label.. ex: "Windows10",
		select Chainloader,
		add partition,
		press "ok" and save grub

	or brutal not raccomended mdoe:
	show all partitions & get the UUID ( exemple of UIDD 5C24-4944 )
	:: sudo blkid or sudo blkid /dev/sda2
	:: sudo gedit /etc/grub.d/40_custom
	menuentry "Windows 10 (UEFI)" {
		search --set=root --file /EFI/Microsoft/Boot/bootmgfw.efi
		chainloader /EFI/Microsoft/Boot/bootmgfw.efi
	}
	
	c - Update Grub
		:: sudo update-grub

##### - Update nvidia drivers

	-remove ex drivers
	:: sudo apt-get purge nvidia* 
	:: sudo apt-get clean
	:: sudo apt-get autoremove
	
	- check actual driver
	:: lspci -nn | egrep -i "3d|display|vga"
	:: sudo find /dev -group video (folder drivers)
	
	- if good:
	:: sudo apt-get install -y nvidia-settings
	
	- if not good:
	  download nvidia driver at: 
	  https://www.nvidia.com/download/index.aspx
	  or
	  https://www.nvidia.com/it-it/drivers/unix/
	
	:: sudo chmod +x NVIDIAxxxx.run
	:: sudo ./NVIDIAxxxx.run --no-x-check

##### - Fix suspend/Ibernate problem (Debian doesn't wakeup) -- not work every

**::**  `sudo apt install lightdm`<br>
**::**  `sudo apt remove light-locker`<br>

##### - Autologin (not work every)

terminal:<br>
**::**  `sudo nano /etc/gdm3/custom.conf` <br>

and edit inside:
	
	WaylandEnable=false<br>
	AutomaticLoginEnable=true<br>
	AutomaticLogin=bertz<br>

##### - remove libreoffice:

**::**  `sudo apt-get remove --purge libreoffice*`<br>
**::**  `sudo apt-get clean`<br>
**::**  `sudo apt-get autoremove`<br>

##### - install snap store

**::**  `sudo apt update`<br>
**::**  `sudo apt install snapd`<br>
**::**  `sudo snap install core`<br>
**::**  `sudo snap install snap-store`<br>

##### - install flat pack store

**::**  `apt install flatpak`<br>
**::**  `apt install gnome-software-plugin-flatpak`<br>
**::**  `flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo`<br>

##### -  install stacer

**::**  `sudo add-apt-repository ppa:oguzhaninan/stacer`<br>
**::**  `sudo apt-get update`<br>
**::**  `sudo apt-get install stacer`<br>

##### - sensor temps

**::**  `apt install hddtemp lm-sensors`<br>
**::**  `apt-cache search lm-sensors`<br>
**::**  `sudo apt update  sudo apt upgrade`<br>
**::**  `sudo sensors-detect`<br>
**::**  `sensors`<br>
**::**  `watch sensors`<br>

add extension: https://extensions.gnome.org/extension/841/freon/<br>

##### - Customization:

install loginized : https://github.com/juhaku/loginized<br>
  *check it:*<br>
   **::**  `sudo apt-get install gnome-tweak-tool`<br>
   **::**  `sudo apt-get install chrome-gnome-shell`<br>
   **::**  `sudo apt-get install gnome-shell-extensions`<br>

	Add Shell Restart: https://extensions.gnome.org/extension/4075/shell-restarter/    
	Add Extension list: https://extensions.gnome.org/extension/3088/extension-list/
	Add Save Workspace Customization: https://extensions.gnome.org/extension/1583/worksets/
	Add Floating Dock: https://extensions.gnome.org/extension/3730/floating-dock/
	
	Add Blur :
		> topbar and windows: https://extensions.gnome.org/extension/4236/blur-me/
		> Lockscreen: https://extensions.gnome.org/extension/2935/control-blur-effect-on-lock-screen/
		> menu and shell (make conflit) https://extensions.gnome.org/extension/3193/blur-my-shell/
	
	Add Control of animation speed: https://extensions.gnome.org/extension/277/impatience/
	Add Desktop icons : https://extensions.gnome.org/extension/1465/desktop-icons/
		Add Remove Arrow : https://extensions.gnome.org/extension/800/remove-dropdown-arrows/
	Add TryIcons no space: https://extensions.gnome.org/extension/355/status-area-horizontal-spacing/
	Add just-perfection : https://extensions.gnome.org/extension/3843/just-perfection/	
	Add Win+Tabs : https://extensions.gnome.org/extension/97/coverflow-alt-tab/
	Add notifications : https://extensions.gnome.org/extension/1526/notification-centerselenium-h/
	Add Service System: https://extensions.gnome.org/extension/1034/services-systemd/
	Add Sound Management: https://extensions.gnome.org/extension/906/sound-output-device-chooser/
