# Lab 4 - Storage

## Windows
Disk 0: partition style GPT, firmware_type UEFI — because it is the primary system drive containing the EFI system partition and Windows boot files.
New disk: partition style GPT — because modern virtual environments and Windows 11 default to GPT for better capacity and partition support.

## Linux layout - before
(paste lsblk-before.txt)

## Linux layout - after the rebuild
(paste the last lsblk)

| Role | Device |
|------|--------|
| Mirror half A | sdb1 |
| Failed half | sdc1 |
| Replacement | sdd1 |

## The question
Your colleague deleted the wrong file from the mirror an hour ago.
Does RAID 1 help? Why?

No, RAID 1 does not help recover a file deleted by mistake. A mirror immediately replicates every deletion command across all drives in the array, destroying the file everywhere simultaneously. Regular backups or snapshot versions would have helped instead.
