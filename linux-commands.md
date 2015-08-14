####APT:
* sudo add-apt-repository ppa:user/ppa-name              __Personal Package Archive__
* sudo apt-get update
* sudo apt-get upgrade
* apt-cache search <pkg>
* apt-cache show <pkg>
* apt-cache policy <pkg>
* sudo apt-get install <pkg>=<version>
* dpkg -l <pkg>

####CHOWN:
* sudo chown -R [owner]:[group] <dir>

####MANAGE DISK:
* sudo fdisk -l
* sudo blkid __shows disk partitions by UUID__
* fstab entry: 
```
UUID=xyz0ad33-c529-481b-b3c4-abc90a449135 /media/<user>/ext-songs ext4 rw,suid,dev,noexec,auto,async 0 2
```
* mount -t ext4 -o rw,suid,dev,noexec,auto,async /dev/sdb7 /media/<user>/ext-songs

####SYSTEM:
* uname -a
* dmidecode
* lscpu
* lspci
  * lspci -vnn
  * lspci -vvx
* sudo lshw
  * sudo lshw -c video
* dmesg
  * dmesg | grep -i 'Graphic\|video\|VGA\|error\|fail'
* modinfo
  * modinfo i915
* wodim --devices
* eject
  * eject -t
  * eject -T
* sudo fdisk -l /dev/sda
* dd if=debian-live-7.8.0-amd64-gnome-desktop.iso of=/dev/sdx bs=4M; sync                __unmount the device /dev/sdx and then proceed__
* dd count=1 bs=512 if=/dev/zero of=/dev/sdx && sync       __restore USB__
* lsblk   __list all drive and partitions in tree format__

####SYSTEM DISPLAY:
* sudo service lightdm restart
* env | grep GDMSESSION
* env | grep DESKTOP_SESSION=
* env | grep XDG_CURRENT_DESKTOP
* glxinfo | grep OpenGL

* dconf dump /org/compiz/
* dconf reset -f /org/compiz/
* setsid unity
* unity --reset-icons

* ~/.config/monitors.xml

* xrandr
* xrandr --output VGA1 --mode 1024x768 --rate 60

* unity-tweak-tool --reset-unity

* sudo dpkg-reconfigure gdm

* /etc/default/grub
* cat /proc/cmdline

####SYSTEM ENV:
* sudo update-alternatives --config java
* sudo update-alternatives --install "/usr/bin/[java|javac|javaws]" "[java|javac|javaws]" "/opt/jdk1.8.0_31/bin/[java|javac|javaws]" 1
* sudo update-alternatives --set [java|javac|javaws] /opt/jdk1.8.0_31/bin/[java|javac|javaws]
* /etc/environment or /etc/profile or ~/.bash_profile or ~/.profile
* export -p __list of all exported variables and functions__

####DESKTOP ENTRY:
```
[Desktop Entry]
Encoding=UTF-8
Version=1.0
Name=Eclipse
Name[en]=Eclipse
Type=Application
Exec=/opt/eclipse/eclipse
Terminal=false
Icon=/opt/eclipse/icon.xpm
Comment=Integrated Development Environment
NoDisplay=false
Categories=Development;IDE;
```
####CLAMAV:
* sudo freshclam
* /etc/clamav/freshclam.conf
  * HTTPProxyServer serveraddress
  * HTTPProxyPort portnumber 
* clamscan -r /home
* clamscan -r --bell -i / __To check all files on the computer, but only display infected files and ring a bell when found__
* clamscan -r /folder/to/scan/ | grep FOUND >> /path/to/save/report/file.txt 
* clamscan -r /home/USER --move=/home/USER/VIRUS 
* clamscan -r /home/USER --remove
* ps ax | grep [c]lamd
* clamdscan -V
* Schedule ClamAV
  * at 3:30 tomorrow
  * at>clamscan -i /home/user | mail user@example.com
  * at> <CTRL-D> 

####VIM:
* u - undo
* ctrl+r - redo

* dmesg |more

####Partitioning:
* Create a new partition table (e.g. "msdos") and filesystem (e.g. EXT4, FAT32) using gparted, or from a terminal:
* For EXT2/3/4 (adjust accordingly), it would be:
  * cfdisk /dev/sdx
  * mkfs.ext4 /dev/sdx1
  * e2label /dev/sdx1 USB_STICK

* For FAT32, install the dosfstools package and run:
  * cfdisk /dev/sdx
  * mkfs.vfat -F32 /dev/sdx1
  * dosfslabel /dev/sdx1 USB_STICK
