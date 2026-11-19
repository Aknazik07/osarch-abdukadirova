Part	                                 What goes in it
Allocation	For each guest: vCPUs, memory, disk size, fixed or dynamically allocated disk, network adapter(s) and mode.
Arithmetic	Your allocation against the figures from Task 1: what is left for the host in CPU, memory and disk. State what you assumed the host itself needs.
Justification	For each choice, why this and not the alternative — in particular the network mode, and anything you set below a minimum.
Verification plan	After both guests are built, which commands — in which guest or on the host — would prove the plan was carried out: the resources each guest actually sees, the SSH connection, the internet access. Give the command and the output you would expect.
# Linux Hardware and System Specifications (VirtualBox VM)

## 1. Processor (lscpu)
Architecture: x86_64
Model name: Intel(R) Celeron(R) N4120 CPU @ 1.10GHz
CPU(s): 1

## 2. Memory / RAM (free -h)
Total: 1.6Gi
Free: 1.0Gi
Available: 1.2Gi

## 3. Storage Disks (lsblk)
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda      8:0    0   25G  0 disk 
├─sda1   8:1    0    1M  0 part 
└─sda2   8:2    0   25G  0 part /

## 4. System & Baseboard (dmidecode)
System Product Name: VirtualBox
OS: Ubuntu 26.04.1 LTS
IPv4 Address: 10.0.2.3
 I set up a virtual machine named ubuntu-server-lab1 using Oracle VM VirtualBox and installed Ubuntu Server 25.04 (64-bit). Resource Allocation Justification When configuring the virtual machine, I allocated 2048 MB (2 GB) of RAM to it. I chose this specific amount because Ubuntu Server runs entirely in a command-line interface without a heavy graphical desktop environment. Because there is no GUI consuming memory in the background, 2 GB is more than sufficient for running terminal commands, updating packages, and practicing basic Linux administration. At the same time, this allocation leaves plenty of free RAM for my Windows host laptop, ensuring that the system remains stable and responsive while running both systems simultaneously. Summary of Lab Steps Before making any core configuration changes, I created a clean baseline snapshot named clean-install. After saving this state, I deliberately broke the system configuration by removing the hostname file to simulate a critical error and verified that the issue persisted. Finally, I performed a rollback operation back to the clean-install snapshot, which successfully restored the virtual machine to its original working state and completely removed all changes.
The primary objective of this laboratory work was to configure a functional virtual network environment using Oracle VirtualBox, establish bidirectional connectivity between guest operating systems (Ubuntu Server and Windows 11), and investigate the resource management behavior of the host operating system under memory overcommitment conditions. Network Configuration and Architecture To achieve guest-to-guest and guest-to-internet communication, the NAT Network (NatNetwork) mode was selected. Unlike standard NAT, which isolates virtual machines into separate private interfaces, a NAT Network establishes a shared virtual switch and a common subnet (10.0.2.0/24). This enables the virtual machines to discover each other directly via IP routing. Furthermore, NAT Network was preferred over a Bridged Adapter to eliminate potential packet drops or connection failures caused by campus Wi-Fi MAC filtering and strict network security policies, while still guaranteeing reliable outbound internet access.

During the network deployment phase, the following IP addresses were assigned via DHCP within the virtual switch: Ubuntu Server 24.04 LTS: 10.0.2.3 (verified via ip a) Windows 11: 10.0.2.15 (verified via ipconfig)

Initial diagnostic tests involving ICMP echo requests (ping) from the Ubuntu Server to Windows 11 resulted in a 100% packet loss. Rather than disabling the host firewall entirely—which introduces significant security vulnerabilities—a granular solution was implemented by creating a specific inbound security rule on Windows 11 to permit ICMPv4-In traffic. Subsequent re-testing confirmed successful bidirectional connectivity with a 0% packet loss rate.

Host Memory Overcommitment Experiment The second phase of the laboratory focused on analyzing host resource constraints. The host computer is equipped with 8.0 GB of physical DDR4 RAM (approximately 7.8 GB usable). An experimental load was introduced by simultaneously allocating 4.0 GB of RAM to both the Ubuntu and Windows virtual machines, creating a scenario where the combined guest demands equaled the total physical capacity of the host.

Under normal baseline conditions (host-memory-before.png), the host operating system utilized approximately 4.0 GB (51%) of its physical memory. However, under peak experimental load (host-memory-after.png), physical RAM utilization surged to 7.1 GB (91%), and the total committed virtual memory expanded to 11.0 out of 11.6 GB. This metric demonstrates that the Windows host successfully prevented out-of-memory crashes by dynamically expanding its paging file (swap space) onto the secondary SSD storage. Once the virtual machine allocations were reduced back to standard operating parameters (host-memory-returned.png), host memory usage safely normalized to approximately 2.5 GB (32%). In summary, Laboratory Work 2 successfully demonstrated the practical implementation of virtual networking topologies and highlighted the critical importance of host resource management, paging mechanisms, and firewall configurations in virtualized environments. All required configuration logs and empirical evidence have been compiled and structured within the repository's evidence.
