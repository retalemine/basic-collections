####SUID, SGID and the Sticky Bits:
* Besides the common read/write/execute rights for the owner/group/others we have 3 extra attributes known as SUID, SGID and Sticky Bits.
* [http://www.codecoffee.com/tipsforlinux/articles/028.html]
* USB sticks/External Devices should be mounted with nodev
* This is what the nodev option prevents – even if somebody creates a world-readable/world-writable device node on their own drive, the OS will refuse to do anything with it because of the nodev option used when mounting.
* The same reasons apply to the nosuid option, which tells the OS to ignore the setuid bit which would normally cause a program to be executed with different privileges than those of the user. For example, /usr/bin/sudo has the setuid bit and is owned by root, so it will always have the same privileges as root does.
