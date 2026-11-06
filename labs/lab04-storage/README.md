# Lab 4 - Storage

## Windows
Disk 0: partition style GPT, firmware_type UEFI — because it is the primary system drive containing the EFI system partition and Windows boot files.
New disk: partition style GPT — because modern virtual environments and Windows 11 default to GPT for better capacity and partition support.

## Linux layout - before
`text
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda      8:0    0   25G  0 disk 
├─sda1   8:1    0    1M  0 part 
├─sda2   8:2    0  1.8G  0 part /boot
└─sda3   8:3    0 23.2G  0 part /
sdb      8:16   0    2G  0 disk 
sdc      8:32   0    2G  0 disk 
sdd      8:48   0    2G  0 disk 
sr0     11:0    1 1024M  0 rom

## Linux layout - after the rebuild
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda       8:0    0   25G  0 disk 
├─sda1    8:1    0    1M  0 part 
├─sda2    8:2    0  1.8G  0 part /boot
└─sda3    8:3    0 23.2G  0 part /
sdb       8:16   0    2G  0 disk 
└─sdb1    8:17   0    2G  0 part 
  └─md0   9:0    0    2G  0 raid1 /mnt/raid1
sdc       8:32   0    2G  0 disk 
└─sdc1    8:33   0    2G  0 part 
sdd       8:48   0    2G  0 disk 
└─sdd1    8:49   0    2G  0 part 
  └─md0   9:0    0    2G  0 raid1 /mnt/raid1
sr0      11:0    1 1024M  0 rom

| Role | Device |
|------|--------|
| Mirror half A | sdb1 |
| Failed half | sdc1 |
| Replacement | sdd1 |

## The question
Your colleague deleted the wrong file from the mirror an hour ago.
Does RAID 1 help? Why?

No, RAID 1 does not help recover a file deleted by mistake. A mirror immediately replicates every deletion command across all drives in the array, destroying the file everywhere simultaneously. Regular backups or snapshot versions would have helped instead.
