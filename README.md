# RemasterLinux

**RemasterLinux Project** - Native Raw copy P2P or Partition to Drive (USB) with compression
https://RemasterLinux.com

**Development methods** and tools required: bash or sh shells + yad gui 2025 | Calamares for Live GUI Installations 2026

GUI User Interface: Both yad gui 0.40.0 gtk2 or yad GUI 10+ gtk3 
	Note: yad GUI 10+ will utilize both --html and --sourceview widgets
		yad GUI 0.40.0 in the SliTazOS Distrubtion will utilize the --html widget
		other yad GUI 0.40.0 distro versions will NOT have either of --html and --sourceview widgets.

**Summary**: To my knowlege no "VERY EASY" GNU-Linux Remaster System exists that just copies raw directories and files unmodified to a target partition (or USB thumb drive). Sure, there are backup tools that allow you to backup and restore data but, these do not Remaster Linux to other partitions and/or other drives; ours will !  Additionally, most Remaster systems are very complicated that even a person like me who has used Debian Linux since 1999 can not accomplish task of remastering "Different Distro Distrubitons". Even worse, some Remaster Tools try to master the "all in one" multi-distro schemea that they end up with a tool that most will not use. 

Every remaster Process should be VERY EASY with the user in mind; and it is very possible and why real programmers choose not to provide easy tools is beyond me. The manual method I use on a daily basis "all the time" as described above will be somewhat easy to automate but, we are not going to use real programming tools. Yes, read that correctly, there will be NO compiling of the RemasterLinux programs and/or scripts. Programs like yad will be compiled by users and we have a process for helper page for yad comiling (Debian based) here: 

**Want to help, Please do !**

Anyone enteresting working on a opensource project with me that Remasters any GNU-Linux OS using bash / sh commands. No chroot | No filesystem.squashfs | After bash proof of concept is proven, UI will be made for all commands using yad GUI - 2 versions 0.40.0 for gtk2 and yad 10+ for gtk3. Here is summary shema of process (just example commands, many other ways, for example: could use dd or rysnc command to copy data). Below process based on Debian and Ubuntu based distros. Would like to cover Arch, Fedora, Antix in the fututre.

**Determine data size** and copy data to a file (img, iso, or )
use partition tool like fdisk or lpart to create a new and formate it to ext2, 3 or 4 to match filesystem of source partiton.
write data image file to new partiton.
get UUID from new partition and insert in to /etc/fstab file
```sudo grub-install (if usb bootable drive) /dev/sdb
sudo mkdir /mnt/sdb
sudo mount /dev/sdb1 /dev/sdb
sudo grub-install –-root-directory=/mnt/sdb/boot/grub /dev/sdb```
Reboot to hard drive grub2 menu
select /dev/sdb and boot it
```sudo grub-mkconfig -o /mnt/sdb/boot/grub/grub.cfg
sudo update-initramfs -u
sudo update-grub```

**These commans are just to accomplish No. 1 above** - Get data total blocks used on a partition and write data to img file:
 ** Example Commands**
```sudo mkdir /mnt/sdb
sudo mount /dev/sdb1 /mnt/sdb
used_blocks=$(df --block-size=1K /mnt/sdb| awk 'NR==2 {print $3}')
result_MB=$(( used_blocks / 512 ))
echo "Used Data for /dev/sdb1: $result_MB"
sudo umount /dev/sdb1
sleep 3
sudo dd if=/dev/sdb1 of=./all_data_usb_sdb1 bs=1MB count=$result_MB status=progress && sync```

**Result: 1 img file written using dd command:**
Used Data for /dev/sdb1: 1778
1761000000 bytes (1.8 GB, 1.6 GiB) copied, 46 s, 38.3 MB/s
1778+0 records in
1778+0 records out
1778000000 bytes (1.8 GB, 1.7 GiB) copied, 46.4529 s, 38.3 MB/s
DIFFICULT Step is No. 2 partition. - I have yet to accomplish this step but, I am close. I would like for users to use gparted, so the 1st release could be use of Gparted to handle partition. Or, It could be Calamares Installer setup (which is over kitll) but, Ultimately, a GUI Installer (Calamares) will be built.
Dedicated website will be https://remasterlinux.com
Feel free to prodive suggestions and ask questions for more detail of the project. TIA Robert
