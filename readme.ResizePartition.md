readme.ResizePartition.md

```
sudo fdisk /dev/mmcblk0
```

```
Command (m for help): p
Disk /dev/mmcblk0: 7.4 GiB, 7948206080 bytes, 15523840 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xea0e7380

Device         Boot  Start     End Sectors  Size Id Type
/dev/mmcblk0p1        8192  131071  122880   60M  c W95 FAT32 (LBA)
/dev/mmcblk0p2      131072 7684095 7553024  3.6G 83 Linux
```
note that the 3.6G partition starts at block 131072
```
Command (m for help): n p 2
Partition type
   p   primary (1 primary, 0 extended, 3 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (2-4, default 2): 2
First sector (2048-15523839, default 2048): 131072
Last sector, +sectors or +size{K,M,G,T,P} (131072-15523839, default 15523839):

Created a new partition 2 of type 'Linux' and of size 7.3 GiB.
```
check again
```
Command (m for help): p

Device         Boot  Start      End  Sectors  Size Id Type
/dev/mmcblk0p1        8192   131071   122880   60M  c W95 FAT32 (LBA)
/dev/mmcblk0p2      131072 15523839 15392768  7.3G 83 Linux
```
Now we need to write it
```
Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Re-reading the partition table failed.: Device or resource busy

The kernel still uses the old table. The new table will be used at the next reboot or after you run partprobe(8) or kpartx(8).
```

```
sudo resize2fs /dev/mmcblk0p2
````
confirm 
```
df -h
```

see:
http://elinux.org/RPi_Resize_Flash_Partitions#Manually_resizing_the_SD_card_on_Raspberry_Pi