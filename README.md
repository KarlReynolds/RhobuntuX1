# RhobuntuX1
Rhobuntu Linux for HTC Kovsky (Sony Ericsson Xperia X1 handset)


View this file in a monospaced font for best readability.
============================================================
RRRRRb, hh             bb                      tt
RR   RR hh       doob  bb      uu   uu nn.nnb, tt    uu   uu 
RRRRRp' hhhhhb, oo  oo bbbbbb, uu   uu nn'  nn tttt  uu   uu 
RR  RR  hh   hh oo  oo bb   bb uu   uu nn   nn tt    uu   uu 
RR   RR hh   hh  doob  bbbbbb  'duub'u nn   nn 'dttt 'duuuX1
          ______ _____  ___ _________  ___ _____ 
          | ___ \  ___|/ _ \|  _  \  \/  ||  ___|
          | |_/ / |__ / /_\ \ | | | .  . || |__  
          |    /|  __||  _  | | | | |\/| ||  __| 
          | |\ \| |___| | | | |/ /| |  | || |___ 
          \_| \_\____/\_| |_/___/ \_|  |_/\____/ 
============================================================

WHAT?
=============
A collection of files that can be used to boot a desktop Linux operating system on the Sony Ericsson Xperia X1 smart phone(codename: HTC Kovsky).
The Rhobuntu operating system is derived from Ubuntu version 8 (Jaunty), which itself is based on Debian Linux.


WHY?
=============
This enables the Xperia X1 smart phone to be used as an ultra mobile personal computer (UMPC) with Linux operating system for low CPU intensity uses such as key management, ssh connections, BBSing, etc.
(Think of a sleek lightweight version of a low power Pandora UMPC)

HOW? 
(Warning: Insufficient technical capability / knowledge can ruin your SD card / Xperia X1 / computer. YOU DO THIS ALL AT YOUR OWN RISK!)
=============

Simple Method (booting from an image file / non-partitioned booting):
--------------------------------------------------------------------------------
-Rename or copy the initrd.gz.BootFromImageFile to be called initrd.gz
-Place the following files in the top directory of a SD memory card and insert into the Xperia X1 SD card slot:
  zImage
  initrd.gz
  Rhobuntu.img
  HARET.EXE
  STARTUP.TXT
-Boot the phone as normal into the Windows mobile operating system.
-(Optional for wifi use) Check settings for MAC address of device. Insert the MAC address of the device in STARTUP.TXT in place of "wl1251_mac=00:AA:CC:DD:EE:FF"
-Open the file manager and navigate to the root of the SD card.
-Run HARET.EXE to boot.

Advanced Method (booting from a partitioned SD card needs superuser privileges on a Linux / Unix based computer):
--------------------------------------------------------------------------------
While logged in as root, or using the sudo prefix to commands...
-Copy the Rhobuntu.img to the Linux or Unix computer. e.g. the temp folder /tmp is used for this example.
  /tmp/Rhobuntu.img
-Create a directory to use as a mount point.
  mkdir -p /tmp/RhobuntuDisk
-Mount the image as a loopback device from the mount point.
   mount -o loop,rw,sync /tmp/Rhobuntu.img /tmp/RhobuntuDisk
-Connect the properly formatted and partitioned SD card to the computer, and ensure the 2nd partition is mounted.
  In testing, a 4Gb card was used with 4 partitions: 2Gb fat32, 2Gb ext2, 250Mb ext2 data, 78Mb ext2 cache. (This partitioning was from previous Kovsky Android ROM cooking, and did not need changing to work with Rhobuntu).
  The 2nd SD card partition should be about 1.5Gb minimum in size. The system files should be under 1Gb total, but extra space is useful for file storage or installing more packages using apt.
  An ext2 format filesytem was used on the partition tested; ext3, and ext4 file systems may also work but are untested.
  For this example the SD card target partition for the filesystem is mounted on /media/sdcard/partition2
-Copy the files from the mounted loopback device to the SD card.
  cp -arxv /tmp/RhobuntuDisk/* /media/sdcard/partition2/
-Unmount the loopback device (you may not wish to unmount immediately if exploring the filesystem / modifiying it on your computer)
  umount /tmp/RhobuntuDisk && rmdir /tmp/RhobuntuDisk
-Rename or copy the initrd.gz.BootFromPartitionedSDcard to be called initrd.gz
-Place the following files in the top directory, of the 1st partition, of the SD memory card, and insert into the Xperia X1 SD card slot:
  zImage
  initrd.gz
  HARET.EXE
  STARTUP.TXT
-Boot the phone as normal into the Windows mobile operating system.
-Check settings for MAC address of device.
-Insert the MAC address of the device in STARTUP.TXT in place of "wl1251_mac=00:AA:CC:DD:EE:FF"
-Open the file manager and navigate to the root of the SD card.
-Run HARET.EXE to boot.


CHANGES since 9.04:
=============
This version includes the updated modules package released with earlier versions.

INITRD.GZ versions created specific to booting from the 1st or 2nd SD card partition. To be used for booting from an image file or separate partition respectively.

Adjustments to STARTUP.TXT for the Kovsky including clock speed. (Overclocking not attempted).

Fatsal's keymap for the Kovsky keyboard implemented.

The image file is no longer referenced as Ubuntu.img, but Rhobuntu.img instead.

Boot loading screen rotated and pause-able infotext added.

Desktop screen orientation scripts adjusted to suit Kovsky display.

Apt software repositories have been updated to http://old-releases.ubuntu.com/ubuntu/ from older Rhobuntu builds, as Ubuntu Jaunty is no longer a current release version.

SSH and Putty SSH client were installed in this version via the package manager.

Files collating personal info were cleaned up, (e.g. /root/.bash_history, wifi config, etc), so generate new ssh keys if required/desired with ssh-keygen.

Filesystem with above changes compiled into a new image file.

Other cosmetic changes, e.g. settings, menu icon, shutdown splash screen, etc were changed.


NOTES:
=============
To set desktop wallpaper background, create the image as Width x Height = 800x480 and place in the root user home directory:
 /root/wallpaper.jpg
 
For the system to see and mount other SD card partitions editing /etc/fstab may be required.

Xpanel key currently appears to sleep the screen with no way investigated to unlock yet. You may wish to modify the keymap to avoid accidental keypresses of the key.

Some users of earlier Rhobuntu versions have reported that non-broadcasting wifi access points cannot be connected to until they broadcast their SSID. This is untested with this build, which connected to a broadcasting access point.

Blackberry style battery pulls to fully switch off, as shutdown will halt once the X server has shutdown. Reboot restarts as expected. Hibernation untested, though possibly similar power state as pressing the Xpanel key (not advised).

Place recalibrate=true in STARTUP.TXT options to run the calibration utility on every boot. 
Alternatively, for one time calibration, once booted: Menu > Run > ts_calibrate
Calibration is stored until next time the calibration utility is run.

Working and not working items are as listed in the Rhobuntu wiki and forum thread. e.g. no camera, bluetooth, infrared mouse.

Interesting aside: The Xperia X1 phone was used by Lisbeth Salander (played by Noomi Rapace) in the film The Girl Who Kicked The Hornet's Nest in the hospital scene.

LINKS:
=============
Rhobuntu wiki:
http://forum.xda-developers.com/wiki/HTC_Rhodium/Ubuntu

Rhobuntu main forum thread on xda-developers:
http://forum.xda-developers.com/showthread.php?t=640785

Xperia X1 (HTC Kovsky) wiki:
http://forum.xda-developers.com/wiki/HTC_Kovsky

Xperia X1 (HTC Kovsky) specification:
http://www.gsmarena.com/sony_ericsson_xperia_x1-2246.php

================================================================================
My thanks to walter79 for making Rhobuntu version 9.04, on which this is based, available once more.
d-signer 2016.
