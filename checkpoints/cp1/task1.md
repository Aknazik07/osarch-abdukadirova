 ## 1a. The computer in front of you

| Figure | This computer | Command it came from |
| :--- | :--- | :--- |
| CPU model | <cpu_model> | wmic cpu get name / Get-CimInstance Win32_Processor \| Select-Object Name |
| Cores / logical processors | <cores> / <logical_processors> | wmic cpu get NumberOfCores,NumberOfLogicalProcessors |
| Hardware virtualization: supported? enabled in firmware? | <supported / enabled> | systeminfo / Get-CimInstance Win32_Processor \| Select-Object VirtualizationFirmwareEnabled |
| Memory: total / available now | <total_ram> / <free_ram> | systeminfo \| findstr /C:"Total Physical Memory" /C:"Available Physical Memory" |
| System disk: size, free space, SSD or HDD | <size>, <free>, <SSD/HDD> | Get-PhysicalDisk and Get-PSDrive C |
| Partition style of the system disk | <GPT / MBR> | Get-Disk \| Select-Object Number,PartitionStyle |
| OS and version | <os_name_and_build> | systeminfo \| findstr /B /C:"OS Name" /C:"OS Version" |

## 1b. A machine you have never seen: a thin-and-light laptop

- *Both guests?*
  Running both Lab 1-2 guests at the same time on this 1b laptop (2 cores / 4 threads, 8 GB RAM, 128 GB eMMC with 31 GB free, Windows 11 Home in S mode) is *no* if their combined resources leave too little for the host.
  - *Host assumptions:* keep at least 1 core / 1 thread free for Windows 11 responsiveness, reserve ~3 GB (3072 MB) RAM for Windows 11 Home in S mode and system overhead, and keep at least ~10-15 GB free on the 31 GB free eMMC so the system does not stall.
  - *CPU arithmetic:* 4 host threads minus <lab1_vcpu + lab2_vcpu> guest vCPUs = <remaining_threads> left (overcommitted if <lab1_vcpu + lab2_vcpu> > 4, and tight on a 1.1 GHz dual-core chip if both run busy workloads at once).
  - *Memory arithmetic:* 8192 MB total RAM - 3072 MB host reserve = 5120 MB available for guests; if <lab1_ram_mb + lab2_ram_mb> > 5120 MB, the host will swap heavily or drop/slow VMs.
  - *Disk arithmetic:* 31 GB free on the 128 GB eMMC - (<lab1_disk_gb + lab2_disk_gb> or actual disk growth) = <remaining_gb> free; with only 31 GB free to start with, running two VMs simultaneously can quickly fill the eMMC.

- *Upgrade first*
  I would change/add *RAM* first if possible, because 8 GB total on a Windows 11 host running VMs hits a hard ceiling fast, followed by *storage space* since 31 GB free on eMMC fills up quickly. However, on this machine both the RAM (8 GB LPDDR4X) and storage (128 GB eMMC) are *soldered to the board*, so nothing can actually be upgraded. Instead, I would run one guest at a time rather than both together, close extra apps on Windows before starting a VM, keep guest sizes small, and store extra files/images externally if needed Aknazik Abdukadirova: CPU model: wmic cpu get name or Get-CimInstance Win32_Processor | Select-Object Name

Cores / logical processors: wmic cpu get NumberOfCores,NumberOfLogicalProcessors

Hardware virtualization (supported / enabled in firmware): systeminfo or Get-CimInstance Win32_Processor | Select-Object VirtualizationFirmwareEnabled

Memory (total / available now): systeminfo | findstr /C:"Total Physical Memory" /C:"Available Physical Memory"

System disk (size, free space, SSD/HDD): Get-PhysicalDisk and Get-PSDrive C

Partition style of the system disk: Get-Disk | Select-Object Number,PartitionStyle

OS and version: systeminfo | findstr /B /C:"OS Name" /C:"OS Version"
Both guests?
Running both Lab 1-2 guests at the same time on this machine (8 GB RAM and 31 GB free on eMMC) probably won't work well if both need noticeable memory and disk space. Out of 8192 MB RAM, around 2560-3072 MB goes to Windows 11 and the hypervisor, leaving roughly 5-5.5 GB for both VMs. If the two guests' RAM plus host overhead goes over 8192 MB or leaves under ~2 GB for Windows, the host will hit heavy swap, lag, or drop processes when memory runs out. With only 31 GB free on the eMMC, two VM disks can also eat up free space fast.Upgrade first:
I would add/change RAM first because 8 GB on a Windows 11 host runs out quickly when running VMs, and then storage space since 31 GB free on the eMMC is tight for two guests. On this laptop, though, the memory and eMMC are soldered to the board, so nothing can actually be upgraded. Instead, I would run one guest at a time rather than both together, close extra apps on Windows before starting a VM, and keep VM disk sizes modest.
