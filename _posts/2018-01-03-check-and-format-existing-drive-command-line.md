---
title: '[Ubuntu] Check and format existing hdd/partition via command line'
author: justudin
---

I want to add new hdd into my existing server, here is how to add it and make the partition and format it to ext4 filesystem.

## First check the drive

Check the drive location:
   ```bash
   sudo lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL
   ```

   would show the following:
   ```bash
	NAME   FSTYPE   SIZE MOUNTPOINT LABEL
	sda           111.8G
	|-sda1 ext4    95.9G /
	|-sda2            1K
	|-sda5 swap    15.9G [SWAP]
	sdb           465.8G
	|-sdb1 ntfs   465.8G
   ```
In my case **sdb** is new added drive.

## Prepare the drive
Using fdisk command:

   ```bash
   sudo fdisk /dev/sdb
   ```

   Now create a new partition, type:
   ```bash
   n
   ```
   Choose partition type (p for primary), type:
   ```bash
   p
   ```
   Enter the partition number.
   ```bash
   1
   ```
   It will ask you to set the start and end cylinders on the disk. Just hit **enter** for each to accept the defaults.
   Change the system type to Linux, type:
   ```bash
   t
   ```
   and 
   ```bash
   83
   ```
   Write the changes to new disk.
   ```bash
   w
   ```

## Format to ext4
Format the new drive into ext4 filesystem.
   ```bash
   sudo mkfs.ext4 /dev/sdb1
   ```
   
## Mount the drive
Now the new partition has been created, you need to mount it **somewhere** to use it. Here I’m using **/mnt/data/**.
First create the directory:
   ```bash
   sudo mkdir /mnt/data/
   ```
   
   and mount it into that directory:
   ```bash
   sudo mount /dev/sdb1 /mnt/data/
   ```

## Mounting the new drive automatically at booting
If you wish to mount the filesystem automatically each time the server boots, adjust the /etc/fstab file:

   ```bash
   sudo nano /etc/fstab
   ```
   
   Add below configuration to the last line.
   ```bash
   /dev/sdb1 /mnt/data ext4 defaults 0 2
   ```

End.
