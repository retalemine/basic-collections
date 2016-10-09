####APT:
* sudo add-apt-repository ppa:user/ppa-name              __Personal Package Archive__
* sudo add-apt-repository --remove ppa:user/ppa-name
* sudo apt-get update
* sudo apt-get upgrade
* sudo apt-get purge <pkg>
* apt-cache search <pkg>
* apt-cache show <pkg>
* apt-cache showpkg <pkg>
* apt-cache policy <pkg>
* apt-cache madison <pkg>
* sudo apt-get install <pkg>=<version>
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

####FILE SYSTEM:
* groups
* cut -d: -f1 /etc/group
* sudo usermod -a -G group_name user_name      __add an user to group__
* sudo chgrp wireshark /usr/bin/dumpcap
* sudo chmod o-rx /usr/bin/dumpcap or chmod 750 /usr/bin/dumpcap
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

####MANAGE DISK:
* sudo fdisk -l
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
* umount /dev/sdb7
* fsck __check filesystem__
* /etc/fstab
* /etc/mtab

####NETWORK:
* ifconfig -a
* curl -L https://parsehub.com/download/linux | tar -xzf - -C /tmp && \
  * sudo mv /tmp/parsehub /opt/ && \
  * sudo ln -s /opt/parsehub/parsehub /usr/local/bin/

####SYSTEM:
* uname -a
* dmidecode
* lscpu
* lspci
  * lspci -vnn
  * lspci -vvx
* sudo lshw
  * sudo lshw -c video
* lsmod
* dmesg
  * dmesg | grep -i 'Graphic\|video\|VGA\|error\|fail'
* modinfo
  * modinfo i915
* wodim --devices
* eject
  * eject -t
  * eject -T
* sudo fdisk -l /dev/sda
* dd if=debian-live-7.8.0-amd64-gnome-desktop.iso of=/dev/sdx bs=4M; sync     __unmount /dev/sdx and then proceed; Also check content of /dev/sdx__
* dd count=1 bs=512 if=/dev/zero of=/dev/sdx && sync       __restore USB__
* lsblk   __list all drive and partitions in tree format__
* printenv
* update-manager         _alt + F2_

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
