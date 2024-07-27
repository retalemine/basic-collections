####APT:
* sudo add-apt-repository ppa:user/ppa-name              __Personal Package Archive__
* sudo add-apt-repository --remove ppa:user/ppa-name
* sudo apt-get update
* sudo apt update
* apt list --upgradable
* apt-key list
* sudo apt-get upgrade
* sudo apt-get remove <pkg>
* sudo apt-get purge <pkg>
* sudo apt-get autoremove
* apt-cache search <pkg>
* apt-cache show <pkg>
* apt-cache showpkg <pkg>
* apt-cache policy <pkg>
* apt-cache madison <pkg>
* sudo apt-get install <pkg>=<version>
* sudo apt-get install --reinstall <pkg>
* dpkg -l <pkg>        __list installed packages__
* dpkg -s <pkg>        __information on package__ 
* sudo dpkg -i <pkg.deb>   __install__
* cat /var/log/dpkg.log | grep "\ install\ "
* sudo apt-get install apt-file
  * sudo apt-file update
  * ldd $HOME/.webex/????/*.so > $HOME/check.txt
  * grep "not found" $HOME/check.txt | sort | uniq
  * apt-file search libXmu.so.6
  * sudo apt-get install -y libxmu6:i386
    * libjawt.so, libgcj16-awt:i386, libgtk2.0-0:i386
    * libpango-1.0-0:i386, libpangoft2-1.0-0:i386, libpangox-1.0-0:i386, libpangoxft-1.0-0:i386, libxft2:i386, libxmu6:i386, libxtst6:i386 __webex__
  * sudo nspluginwrapper -i /usr/lib/jvm/ia32-java-6-sun/jre/lib/i386/libnpjp2.so
  * ln -sf <<dir>>/lib/i386/libnpjp2.so ~/.mozilla/plugins/

####Pac:
* pacman -S package_name1 package_name2 ...		__install a single package or list of packages__
* pacman -S extra/package_name 					__Sometimes there are multiple versions of a package in different repositories, e.g. extra and testing__
* pacman -Sg gnome								__list packages belong to the gnome group__
* pacman -Syu 									__Upgrading packages__
* pacman -Ss string1 string2 ...				__search__
* pacman -Ss '^vim-'
* pacman -Qs string1 string2 ...				__search already installed packages__
* pacman -Si package_name 						__display extensive information __
* pacman -Qi package_name 						__locally installed packages__
* pactree package_name 							__list a dependency tree of a package__
* pacman -Sc									__Cleaning the package cache @ /var/cache/pacman/pkg/__
* pacman -Scc									__empty the cache folder fully__
* pacman -Sw package_name	 					__Download a package without installing it__
* pacman -Fy									__Sync the files database__
* pacman -Fs pacman								__Search for a package containing a file__
* pacman -Syy  									__To ensure you have list from primary mirror__
* pacman -Syu  									__To download packages.__
* pacman -Syyu 									__first refreshes using primary mirror and then updates__
* pacman -U <package name>.pkg.tar 				__install specific package from tar file__

####FILE SYSTEM:
* groups
* cut -d: -f1 /etc/group
* grep -i --color 'docker' /etc/group
* members group-name
* sudo usermod -a -G group_name user_name      __add an user to group__
* sudo chgrp wireshark /usr/bin/dumpcap
* sudo chmod o-rx /usr/bin/dumpcap or chmod 750 /usr/bin/dumpcap
* sudo chmod [ugo][+-][rwx] <file>
* sudo setcap 'CAP_NET_RAW+eip CAP_NET_ADMIN+eip' /usr/bin/dumpcap
* sudo getcap /usr/bin/dumpcap
* sudo chown -R [owner]:[group] <dir>
* grep -rnw '/path/' -e "pattern"      __ -r recursive, -n line number, -w whole word, -l file name__
* grep --include=\*.{c,h} -rnw '/path/to/somewhere/' -e "pattern"
* grep --exclude=*.o -rnw '/path/to/somewhere/' -e "pattern"
* grep --exclude-dir={dir1,dir2,*.dst} -rnw '/path/to/somewhere/' -e "pattern"
* grep -v 'string' file __does inverse__
* find dir/ -type f -exec grep -H 'string' {} +
* find . -type f -iname '*.ini' -exec cp --parent \{\} /<path>/ \;
* find . -type f -iname '*.ini' -print -delete
* find . -type d -empty -exec rmdir {} \;
* find . -name *.png -type f -print | xargs tar -cvzf images.tar.gz
* find . -type f ! -path '*/node_modules/*'
* find . -type f ! -path '*/.git/*'
* ls /etc/*.conf | xargs -i cp {} /home/likegeeks/Desktop/out
* cp -vur * /destination
* du -sh   __b/k/m/g/t/p__
* sha1sum file.ext > file.sha1
* cat file.sha1 | sha1sum -c -
* locale
  * locale -a
  * locale charmap
* file limited.csv
  * file -bi limited.csv
* hexdump -n 128 -C limited.csv
* free -h
* top -b -n 1 | grep 'lightdm'

####MANAGE DISK:
* sudo fdisk -l
* sudo hdparm -i /dev/sda | grep Model
* sudo parted -l
* sudo gdisk -l /dev/sda
* sudo blkid __shows disk partitions by UUID__
* fstab entry:   __wiki.debian.org/fstab__
```
UUID=xyz0ad33-c529-481b-b3c4-abc90a449135 /media/<user>/ext-songs ext4 rw,suid,  dev,  noexec,auto,async     0 2
/dev/sdb5                                 /media/<user>/eData     ext4 rw,nosuid,nodev,relatime,data=ordered 0 0
```
* mount -t ext4 -o rw,suid,  dev,  noexec,auto,async /dev/sdb7 /media/<user>/ext-songs
* mount -t ext4 -o ro,nosuid,nodev,noexec,auto,async /dev/sdb5 /media/<user>/ext-data
* sudo apt-get install mkusb mkusb-nox usb-pack-efi
* sudo mount -o loop /media/user/usb/casper-rw /mnt/livedrive
* umount /dev/sdb7
* mount | column -t
* fsck __check filesystem__
* sudo fsck -t ext4 -y -f -c /dev/sdb1    __answer y; force check;__
* sudo fsck -l bad-blocks /dev/sdb1       __?__
* sudo e2fsck -l badblocks.log /dev/sda1
* sudo badblocks -sv /dev/sdb1 __-w destructive__
* /etc/fstab
* /etc/mtab

####NETWORK:
* ifconfig -a
* curl -L https://parsehub.com/download/linux | tar -xzf - -C /tmp && \
  * sudo mv /tmp/parsehub /opt/ && \
  * sudo ln -s /opt/parsehub/parsehub /usr/local/bin/
* ethtool eth0
* ethtool -i ethX
* netstat -i
* ifconfig -a
* ifconfig up eth0
* ip link show
* ip addr 
* cat /sys/class/net/enp4s0/carrier
* cat /sys/class/net/enp4s0/operstate

####SYSTEM:
* uname -a
* dmidecode
* lscpu
* lspci
  * lspci -vnn
  * lspci -vvx
  * lspci -[v|k]
  * lspci -v -s 00:02.0
  * lspci | grep -i --color 'vga|3d|2d' | less
* sudo lshw
  * sudo lshw -c video
* lsmod
* dmesg
  * dmesg | grep -i 'Graphic\|video\|VGA\|error\|fail'
* cat /sys/kernel/debug/vgaswitcheroo/switch   __List GPU providers__
* modinfo
  * modinfo i915
* wodim --devices
* eject
  * eject -t
  * eject -T
* sudo fdisk -l /dev/sda
* dd if=debian-live-7.8.0-amd64-gnome-desktop.iso of=/dev/sdx bs=4M status=progress && sync     __unmount /dev/sdx and then proceed; Also check content of /dev/sdx__
* dd bs=4M if=MX-19.3_ahs_x64.iso of=/dev/sdc status=progress oflag=sync
* dd count=1 bs=512 if=/dev/zero of=/dev/sdx && sync       __restore USB__
* dd if=/dev/urandom of=/dev/null status=progress
* sudo dd if=/dev/foo bs=4M | pv -s 20G | sudo dd of=/dev/baz bs=4M
* sudo dd if=/dev/sdc conv=sync,noerror bs=64K  | gzip -c > /data/torrent/OS/en_windows_7_professional_with_sp1_x64_dvd_u_676939.img.gz
* sudo dd if=/dev/sdc conv=sync,noerror bs=64K  of=/data/torrent/OS/en_windows_7_professional_with_sp1_x64_dvd_u_676939.img status=progress
* gzip -k /data/torrent/OS/en_windows_7_professional_with_sp1_x64_dvd_u_676939.img
* sudo dd if=/dev/sdx conv=sync,noerror bs=64K  of=/dev/sdb status=progress
* sudo dd if=/dev/sdx conv=sync,noerror bs=128K | gzip -c | ssh vivek@server1.cyberciti.biz dd of=centos-core-7.gz
* sudo dd if=/dev/sdx iflag=fullblock of=/path/to/new.iso status=progress
* gunzip -c /mnt/external_disk/backup_image.img.gz | dd of=/dev/sdx
* fdisk –l /data/torrent/OS/en_windows_7_professional_with_sp1_x64_dvd_u_676939.img
* pv /home/user/bigfile.iso | md5sum
* sudo kill -SIGUSR1 $(pidof dd)
* lsusb -v
  * lsusb -s 001:006 -v
* dc3dd if=/dev/sda of=/dev/sdb
  * sudo ddrescue -v /dev/sda /dev/sdb
* dd if=infile | pv > outfile
  * pv infile > outfile
  * sudo pv /dev/sda1 > /home/user/sda1.ext4.img
* testdisk - Partition scanner and disk recovery tool, and PhotoRec file recovery tool
* lsblk   __list all drive and partitions in tree format__
* printenv
* update-manager         _alt + F2_
* systemd-analyze blame

####SYSTEM DISPLAY:
* sudo service lightdm restart
* systemctl status lightdm.service
* sudo dpkg-reconfigure lightdm
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
* xrandr --listproviders

* unity-tweak-tool --reset-unity

* sudo dpkg-reconfigure gdm

* /etc/default/grub
* cat /proc/cmdline

####SYSTEM ENV:
* sudo update-alternatives --config java
* sudo update-alternatives --install "/usr/bin/[java|javac|javaws]" "[java|javac|javaws]" "/opt/jdk1.8.0_31/bin/[java|javac|javaws]" 1
* sudo update-alternatives --set [java|javac|javaws] /opt/jdk1.8.0_31/bin/[java|javac|javaws]
* /etc/environment or /etc/profile or ~/.bash_profile or ~/.profile
  * /etc/profile.d/ /etc/ld.so.conf.d/
* export -p __list of all exported variables and functions__
* ldconfig -[p|v] _library list_
* ldconfig -n /opt/dummy/lib _Please note that this doesn’t rebuild the cache. It just updates the link._

####DESKTOP ENTRY:
* /usr/share/applications
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

```
[Desktop Entry]
Version=1.0
Type=Application
Name=PyCharm Community Edition
Icon=/opt/programfiles/pycharm-community-2017.1.3/bin/pycharm.png
Exec="/opt/programfiles/pycharm-community-2017.1.3/bin/pycharm.sh" %f
Comment=The Drive to Develop
Categories=Development;IDE;
Terminal=false
StartupWMClass=jetbrains-pycharm-ce
```

```
/home/subhu/.local/share/applications/
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
* sudo clamscan -r -z -v -i --bell -l /home/subhu/Documents/clamav-reports/temp.log .
* ps ax | grep [c]lamd
* clamdscan -V
* Schedule ClamAV
  * at 3:30 tomorrow
  * at>clamscan -i /home/user | mail user@example.com
  * at> <CTRL-D> 

####VIM:
* u - undo
* ctrl+r - redo
* :1,$d - delete every line

* dmesg |more
* tee

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

####Boot Space Clean Up:
* df -h
* watch df -h
* du -sk * | sort -n
* apt-get autoremove
* apt-get clean				_/var/cache/apt/archives/ and /var/cache/apt/archives/partial/_
* uname -r  _To know the kernel version currently used_
* dpkg -l linux-image-\* | grep ^ii  _To list all installed kernels_
* kernelver=$(uname -r | sed -r 's/-[a-z]+//')
  * dpkg -l linux-{image,headers}-"[0-9]*" | awk '/ii/{print $2}' | grep -ve $kernelver  _command to show all kernels and headers that can be removed, excluding the current running kernel_
* sudo apt-get purge $(dpkg -l linux-{image,headers}-"[0-9]*" | awk '/ii/{print $2}' | grep -ve "$(uname -r | sed -r 's/-[a-z]+//')")  _command to purge all but running kernel version_ _avoid_
```
sudo apt-get purge linux-image-{3.0.0-12,2.6.3{1-21,2-25,8-{1[012],8}}}-generic
sudo apt-get purge linux-image-3.5.0-{17,18,19,21,22,23,24}
sudo apt-get purge linux-headers-3.19.0-30 linux-image-3.19.0-30-generic
```

####Virutal Box:
* VBoxManage list -l vms

####Network File Sharing:
* sudo apt-get install samba
* sudo smbpasswd -a <user_name>
* mkdir /home/<user_name>/<share_folder_name>
* sudo nano /etc/samba/smb.conf
   security = user
[share_folder_name]
    comment = Ubuntu File Server Share Gallery
    path = /media/subhu/ext-backup/gallery
	valid users = subhu
    browsable = yes
    guest ok = no
    read only = no
    create mask = 0744
* sudo service smbd restart
* testparm
* sudo apt-get install smbclient
* List all shares:
  * smbclient -L //<HOST_IP_OR_NAME>/ -U <user>
  * smbclient -L //192.168.1.4 -U subhu -N
  * smbclient -d3 -L //192.168.1.4 -U subhu -N
* connect:
  * smbclient //<HOST_IP_OR_NAME>/<folder_name> -U <user>
* Alt+F2 prompt
  * "smb://<HOST_IP_OR_NAME>/<folder_name>/" (Linux users) and "\\<HOST_IP_OR_NAME>\<folder_name>\" (Windows users)
* Note: The default user group of samba is "WORKGROUP".
* sudo apt-get install cifs-utils
  * mkdir ~/Desktop/Windows-Share
  * sudo mount.cifs //WindowsPC/Share /home/geek/Desktop/Windows-Share -o user=geek
* sudo apt-get install libpam-smbpass
  * libpam-smbpass package will sync system users and passwords with the Samba user database.
```
Error returning browse list: NT_STATUS_ACCESS_DENIED
Connection to 192.168.1.2 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
NetBIOS over TCP disabled -- no workgroup available
```
* Cause
  * One possible reason for this issue is that the “User Account Control: Run all Administrators in Admin Approval Mode” security option is enabled on the Windows 7 system.
* Resolution
  * Disable the “User Account Control: Run all Administrators in Admin Approval Mode” security option using the following steps:
    1) Click on the START button and type gpedit.msc
    2) Browse to Computer Configuration | Windows Settings | Security Settings | Local Policies | Security Options
    3) Disable the “User Account Control: Run all Administrators in Admin Approval Mode” policy.

####Youtube-dl:
* youtube-dl -j --flat-playlist https://www.y.com/playlist?list=PLSM7v62fgiGEA1S80Hra3BJDmD3oWKdJF | jq -r '.id' | sed 's_^_https://youtube.com/v/_'
* youtube-dl -F --youtube-skip-dash-manifest https://www.youtube.com/watch?v=Jn-GwAN2Ahk
* youtube-dl -f 22 https://www.youtube.com/watch?v=Jn-GwAN2Ahk
* youtube-dl --list-formats https://www.youtube.com/watch?v=Jn-GwAN2Ahk
* youtube-dl https://www.youtube.com/playlist?list=PLSM7v62fgiGEA1S80Hra3BJDmD3oWKdJF
* youtube-dl -x --audio-format mp3 --audio-quality 128k https://www.youtube.com/watch?v=xyz
```
--verbose
--print-traffic
--list-extractors
--flat-playlist
--list-formats
--youtube-skip-dash-manifest
-k
-j
-F
-f
-o "%(id)s"
```

####Clean Up:
* rm ~/.local/share/zeitgeist/activity.sqlite
  * zeitgeist-daemon --replace

####Verify Signature:
* gpg --keyserver pool.sks-keyservers.net --recv-keys 0x4E2C6E8793298290
* gpg --fingerprint 0x4E2C6E8793298290
* gpg --verify ~/Downloads/tor-browser-linux64-6.0.5_en-US.tar.xz{.asc,}

####Detecting available microcode update: 
* sudo update-pciids			_grab the current version of the pci.ids file from the Internet_

1) sudo apt-get install iucode-tool (skip extra package intel-microcode; would say intel-microcode: microcode will be updated at next boot)
2) iucode_tool -K/tmp/microdir/ ~/Downloads/microcode.dat
3) modprobe cpuid && iucode_tool -tb -lS /tmp/microdir
	* iucode_tool: could not open cpuid devices, cannot scan system processor signatures ??
	* Should the signature scan fail on all online processors, the program  will  print  a  warning  to  the  user  and  continue  as  if --scan-system had not been specified.  This is a fail‐safe condition when iucode_tool is used to install microcode updates for the next boot.

####Processor Update:
* https://wiki.debian.org/Microcode
* update-intel-microcode - download current Intel processor microcode
* lsmod | grep microcode
* dmesg | grep microcode			_Verifying that microcode got updated on boot_
[    0.000000] CPU0 microcode updated early to revision 0xa0b, date = 2010-09-28
[    0.008000] CPU1 microcode updated early to revision 0xa0b, date = 2010-09-28
[    0.475475] microcode: CPU0 sig=0x1067a, pf=0x1, revision=0xa0b
[    0.475477] microcode: CPU1 sig=0x1067a, pf=0x1, revision=0xa0b
[    0.475577] microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba
* journalctl -b | grep microcode
* journalctl -b -1 
Dec 31 21:29:27 subhu-desktop kernel: CPU0 microcode updated early to revision 0xa0b, date = 2010-09-28
Dec 31 21:29:27 subhu-desktop kernel: CPU1 microcode updated early to revision 0xa0b, date = 2010-09-28
Dec 31 21:29:27 subhu-desktop kernel: microcode: CPU0 sig=0x1067a, pf=0x1, revision=0xa0b
Dec 31 21:29:27 subhu-desktop kernel: microcode: CPU1 sig=0x1067a, pf=0x1, revision=0xa0b
Dec 31 21:29:27 subhu-desktop kernel: microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba

####GPU benchmarking tools:
* sudo apt-get install mesa-utils
* glxgears -info
  * DRI_PRIME=1 glxgears -info
* sudo apt-get install glmark2
* glmark2
* GpuTest is a cross-platform (Windows, Linux and Max OS X) GPU stress test and OpenGL benchmark. 
https://help.ubuntu.com/community/RadeonDriver
https://help.ubuntu.com/community/BinaryDriverHowto/AMD
http://unigine.com/products/benchmarks/heaven/

!!!
$ sudo update-pciids			_grab the current version of the pci.ids file from the Internet_

$ inxi -M
$ inxi -G

$ sudo lshw
$ sudo lshw -short
$ sudo lshw -class display

$ sudo dmidecode -t baseboard

$ lscpu

$ grep -i --color memory /var/log/Xorg.0.log
$ sudo dmesg | grep drm

$ hardinfo

$ glxinfo | grep OpenGL	
$ LIBGL_DEBUG=verbose glxinfo
	Make sure your OpenGL renderer string does not say "software rasterizer" or "llvmpipe" because that would mean you have no 3D hardware acceleration

* The "OpenGL renderer string" if points to MESA libraries means that 3d rendering is being handled entirely inside software. This is going to be slow and games would not work well.
* To get clock speed information
  * For ATI/AMD GPUs, aticonfig --odgc will fetch the clock rates, and aticonfig --odgt will fetch the temperature data.
  * For NVIDIA GPUs, the nvclock program will fetch the same information.
* If fglrx is installed and working well you should see an output similar to:
$ fglrxinfo
display: :0  screen: 0
OpenGL vendor string: Advanced Micro Devices, Inc.
OpenGL renderer string: ATI Radeon HD 4300/4500 Series       
OpenGL version string: 3.3.11399 Compatibility Profile Context

$ modinfo i915 				_check the detail of the video driver_

$ dmesg | grep -i 'Graphic\|video\|VGA\|error\|fail\|drm\|radeon\|amd\|gpu|\mux'

$ dpkg -l | grep 'nvidia\|AMD\|ATI'

$ sensors

$ xrandr --listproviders

$ lsb_release -a
~~~~~~~~~~~~~~~~~~~~~~~``
$ sudo grep -i switcheroo /boot/config-*
	/boot/config-4.1.0-1-amd64:CONFIG_VGA_SWITCHEROO=y
	vga_switcheroo is the kernel mechanism that allows you to switch between GPUs if your machine has a hardware mux. And only works if you are using the opensource driver.
$ sudo gedit /etc/default/grub => "modeset=1" kernel option, and/or the "nomodeset" option being absent for vga_switcheroo to work
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash radeon.modeset=1"
$ sudo update-grub
$ sudo ls -l /sys/kernel/debug/vgaswitcheroo/switch	_To test if vga_switcheroo is enabled, look for the switch file_
$ sudo cat /sys/kernel/debug/vgaswitcheroo/switch
	Allows you to verify the current state of the hybrid graphics. Typically, there will be two lines of output - one should indicate "Pwr" and the other should indicate "Off".
$ sudo su
$ sudo echo ON > /sys/kernel/debug/vgaswitcheroo/switch
	Turns on the GPU that is disconnected (not currently driving outputs), but does not switch outputs.
$ sudo echo IGD > /sys/kernel/debug/vgaswitcheroo/switch
	Connects integrated graphics with outputs.
$ sudo echo DIS > /sys/kernel/debug/vgaswitcheroo/switch
	Connects discrete graphics with outputs.
$ sudo echo OFF > /sys/kernel/debug/vgaswitcheroo/switch
	Turns off the graphics card that is currently disconnected.
$ sudo echo DIGD > /sys/kernel/debug/vgaswitcheroo/switch
	Queues a switch to integrated graphics to occur when the X server is next restarted.
$ sudo echo DDIS > /sys/kernel/debug/vgaswitcheroo/switch
	Queues a switch to discrete graphics to occur when the X server is next restarted.
~~~~~~~~~~~~~~~~~~~~~~~``
~~~~~~~~~~~~~~~~~~``
$ amdconfig --uninstall				_Uninstall the driver you installed from the AMD/ATI website_
$ /usr/share/ati/amd-uninstall.sh --force
$ apt-get purge fglrx fglrx-updates fglrx-amdcccle fglrx-amdcccle-updates
$ rm /usr/share/ati

reconfigure:
$ apt-get install --reinstall xserver-xorg-core libgl1-mesa-glx libgl1-mesa-dri
$ dpkg-reconfigure xserver-xorg
$ update-initramfs -u

$ mv /etc/X11/xorg.conf /etc/X11/xorg.conf.bak			_remove any conf if it was created when you installed fglrx_

$ apt-get remove vgaswitcheroo			_uninstall vga_switcheroo_
!!!

####ISO to IMG:
* Delete all partitions, create a new one taking up all the space, set type to NTFS (7), and remember to set it bootable:
  * cfdisk /dev/sdb   or   fdisk /dev/sdb (partition type 7, and bootable flag)
* Create an NTFS filesystem:
  * mkfs.ntfs -f /dev/sdb1
* Write Windows 7 MBR on the USB stick (also works for windows 8), multiple options here:
  * ms-sys -7 /dev/sdb
  or (e.g. on newer Ubuntu installs) sudo lilo -M  /dev/sdb mbr (info)
  or (if syslinux is installed) sudo dd if=/usr/lib/syslinux/bios/mbr.bin of=/dev/sdb
* Mount ISO and USB media:
  * mount -o loop win7.iso /mnt/iso
  * mount /dev/sdb1 /mnt/usb
* Mount & Execute:
  * mkdir -p /tmp/cdrom
  * mount -o loop,exec /path/to/systemrescuecd-x86-x.y.z.iso /tmp/cdrom
  * cd /tmp/cdrom
  * bash ./usb_inst.sh
  * cd ~
  * umount /tmp/cdrom
* Copy over all files:
  * cp -r /mnt/iso/* /mnt/usb/   ...or use the standard GUI file-browser of your system
* Call sync to make sure all files are written.
* dd if=/dev/sdb of=/win7.img
* reverse if/of next time you want to put the Windows 7 installer onto USB.


sudo ufw status
sudo setterm --dump 1 --file screen.dump

sudo -i ethtool enp3s1
sudo -i ethtool -S enp3s1
ethtool eth0 | grep Wake-on

ip addr
ip link
ip link show up
netstat -nr
arp -e

ifconfig up enp3s1

sudo dhclient -v enp3s1 

ping www.google.com
whois yahoo.com
traceroute -I 144.232.20.158
tracert 80.40.118.227
mtr 192.168.25.26
tcpdump -i wlan0 -t host 192.168.1.102 and tcp port 22
tcpdump -i eth1 -w /tmp/packets.dump tcp port 22
tshark -i eth0 tcp port 80 and host 192.168.1.100
nslookup www.linuxhomenetworking.com

sudo lsof -i
netstat -nr
netstat -g
netstat -aop | grep "18489"
netstat -nutcpawl | grep EST

cat /sys/class/net/enp3s1/operstate
cat /sys/class/net/enp3s1/carrier
cat /etc/network/interfaces
cat /etc/hosts
cat /etc/resolv.conf

mount /media/cdrom -o unhide
umount /media/cdrom
eject cdrom

####System Info:
sudo apt-get install lm-sensors
mkdir -p ~/Desktop/systeminfo
dmesg > ~/Desktop/systeminfo/init-dmesg.txt
dpkg -l > ~/Desktop/systeminfo/dpkg-list.txt
sudo fdisk -l > ~/Desktop/systeminfo/fdisk.txt
lsblk > ~/Desktop/systeminfo/lsblk.txt
cat /etc/fstab > ~/Desktop/systeminfo/fstab.txt
cat /etc/mtab > ~/Desktop/systeminfo/mtab.txt
uname -a > ~/Desktop/systeminfo/uname.txt
lsb_release -a > ~/Desktop/systeminfo/lsb.txt
cat /etc/os-release >> ~/Desktop/systeminfo/lsb.txt
cat /etc/issue >> ~/Desktop/systeminfo/lsb.txt
cat /proc/cmdline > ~/Desktop/systeminfo/cmdline.txt
cat /etc/default/grub > ~/Desktop/systeminfo/grub.txt
printenv > ~/Desktop/systeminfo/env.txt
ifconfig -a > ~/Desktop/systeminfo/ifconfig.txt
sudo dmidecode > ~/Desktop/systeminfo/dmidecode.txt
sudo lscpu > ~/Desktop/systeminfo/lscpu.txt
sudo lspci -vvnn > ~/Desktop/systeminfo/lspci.txt
sudo lshw > ~/Desktop/systeminfo/lshw.txt
lsmod > ~/Desktop/systeminfo/lsmod.txt
wodim --devices > ~/Desktop/systeminfo/wodim.txt
sensors > ~/Desktop/systeminfo/sensors.txt
inxi -v7 > ~/Desktop/systeminfo/inxi.txt
sudo cat /sys/kernel/debug/vgaswitcheroo/switch > ~/Desktop/systeminfo/vgaswitch.txt
xrandr > ~/Desktop/systeminfo/xrandr.txt
xrandr --listproviders >> ~/Desktop/systeminfo/xrandr.txt
glxinfo | grep OpenGL > ~/Desktop/systeminfo/openGL.txt
xinput > ~/Desktop/systeminfo/xinput.txt
cat /proc/interrupts > ~/Desktop/systeminfo/interrupts.txt
cat /proc/acpi/wakeup > ~/Desktop/systeminfo/wakeup.txt
pstree > ~/Desktop/systeminfo/pstree.txt
echo $PATH >  ~/Desktop/systeminfo/PATH.txt

ACPI - Advanced Configuration and Power Interface
APM - Application Performance Monitoring
acpi - displays information on ACPI devices
acpitool - command line ACPI client
apmd - Utilities for Advanced Power Management (APM)
acpidump - go to the tools/power/acpi/ directory of your kernel source code and run “make”.
impitool <relevant connection options> sel list (?)
systemd
dmesg -k
journalctl | less
ACPI_NOTIFY_DEVICE_WAKE
$ pstree
$ last 100
$ last -x reboot 
$ who
$ who -b 

curl -L https://parsehub.com/static/client/parsehub.tar.gz | tar -xzf - -C /tmp && \
sudo mv /tmp/parsehub /opt/ && \
sudo ln -s /opt/parsehub/parsehub /usr/local/bin/

File Content Handling:
* Merge
  * join -1 1 -2 1 --header --nocheck-order -t , -i file1 file2
  * join -1 1 -2 1 --check-order -t , -i file1 file2
  * join -a 1 -a 1 -e " " file1 file2
  * join -v
  * join -t , --nocheck-order -j 1 ms.txt ru.txt > /tmp/msru-1.txt \ cat /tmp/msru-1.txt | wc -l 
  * join -t , --nocheck-order -a 1 ms.txt ru.txt > /tmp/msru-2.txt \ cat /tmp/msru-2.txt | wc -l
  * join -t , --nocheck-order -a 2 ms.txt ru.txt > /tmp/msru-2-2.txt \ cat /tmp/msru-2-2.txt | wc -l
  * join -t , --nocheck-order -v 1 ms.txt ru.txt > /tmp/msru-3.txt \ cat /tmp/msru-3.txt | wc -l
  * join -t , --nocheck-order -v 2 ms.txt ru.txt > /tmp/msru-3-2.txt \ cat /tmp/msru-3-2.txt | wc -l
* Horizontal
  * paste -d ',' file1 file2 file3 ...
* Vertical
  * dd if=file2 of=file2 bs=1M count=10 oflag=append conv=notrunc
  * cat input1.csv input2.csv input3.csv > combined.csv
  * cat file1 file2 file3 | tee -a file4 > /dev/null
  * cat input1.csv > combined.csv \ cat input2.csv | sed "1 d" >> combined.csv \ cat input3.csv | sed "1 d" >> combined.csv
* Selection
  * dd if=file1 of=file2 bs=1M count=99 skip=1
  * cut -d , -f 2,4-6 input.csv
  * (head -n 1 run_results-fundsnapshot.csv && tail -n +2 run_results-fundsnapshot.csv | sort)
  * head -n 1 run_results-fundsnapshot.csv
* Conversion
  * dd if=file1 of=bigfile2 seek=$(stat -c %s bigfile2)
  * dd if=file1 of=file2 conv=ucase
  * dd if=textfile.ebcdic of=textfile.ascii conv=ascii
  * cat file.in | tr a-z A-Z > file.out
  * cat file.in | tr ':[space]:' '\t' > file.out
* Creation
  * dd if=/dev/zero of=out.txt bs=1M count=10

####OS Migration:
* Puddletag
./.config/puddletag
./.local/share/puddletag

####LTS
* sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup
  * http://us.archive.ubuntu.com/ubuntu/ or http://security.ubuntu.com/ubuntu  to http://old-releases.ubuntu.com/ubuntu/
