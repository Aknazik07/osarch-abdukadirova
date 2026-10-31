# Ticket 1 - New developer starts Monday, needs a test machine

## 1. What was asked

> From: Aigerim T. (Office Manager)
> Subject: test machine for new dev
> 
> Hi, we have someone starting on Monday and he needs a test computer set up. Nothing special, just so he can try things without breaking anything. Can you write down how to do it so I can do the next one myself? Thanks
## 2. What was actually needed

The initial request omitted crucial technical parameters required to set up a functional virtual machine. Specifically, it did not specify which operating system distribution to install, the core count, the storage size, or the required RAM limits. Furthermore, it failed to mention network requirements (whether isolated or connected to the internet) and host resource constraints. 

Instead of asking the office manager technical questions, I assumed standard safe defaults suitable for a test environment: an Ubuntu Server guest, 2 GB of RAM, and a 25 GB virtual hard disk, which safely fits within the available resources of my host laptop (Acer TravelMate Spin B3 with 8 GB RAM). I chose a NAT network adapter to ensure safe internet access without exposing the guest directly to external networks.
## 3. What I did

1. Opened Oracle VirtualBox on the host system.
2. Created a new virtual machine named 'ubuntu-server-lab1' and allocated 2 GB of RAM and 25 GB of dynamically allocated virtual storage, balancing performance with the host's 8 GB physical memory limit.
3. Configured the VM network adapter in NAT mode during initial creation to provide secure internet access while keeping the host isolated.
4. Attached the Ubuntu Server ISO image and performed a clean installation of the operating system with active internet connectivity.In VirtualBox, go to Settings > Storage. Under the Optical Drive controller, select Choose a disk file and attach the downloaded Ubuntu Server ISO image. Reasoning: This mounts the operating system installer into the VM's virtual CD/DVD drive so the system can boot from it and start the installation process.
5. Logged into the guest OS and verified system parameters (RAM, disk size) and network connectivity using command-line tools (free -h, df -h, lsblk, ip addr).
## 5. What I would do differently

"During this build, leaving the network adapter enabled during OS installation caused additional delays while the installer fetched packages online. In the future, I would disconnect the network adapter during initial setup to speed up the installation process, and enable NAT/DHCP only after the first successful boot."
