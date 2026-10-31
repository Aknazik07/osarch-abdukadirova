# Build Guide: Ubuntu Server Virtual Machine Setup

This guide provides step-by-step instructions for deploying an Ubuntu Server virtual machine using Oracle VirtualBox. Each configuration step includes specific technical rationale and explains why particular options were chosen over defaults.

---

## 1. Prerequisites and Host Resource Analysis
- Host System: Windows 11 running on a physical host laptop (Acer TravelMate Spin B3) equipped with 8 GB of physical RAM and an Intel 4-core processor.
  - Rationale: 8 GB of total host RAM is a strict hardware constraint. When provisioning virtual machines, we must carefully calculate resource allocation to prevent host system memory starvation and ensure stable multitasking.
- Hypervisor: Oracle VirtualBox.
  - Rationale: Chosen as a reliable, lightweight Type-2 hypervisor that integrates natively with Windows 11 without requiring commercial licensing.
- Installation Media: Official Ubuntu Server 24.04 LTS ISO image.
  - Rationale: Selected for its enterprise-grade stability, long-term support (LTS), and headless optimization, making it ideal for CLI-based server environments.

---

## 2. Step-by-Step Build Procedure

### Step 1: Create New Virtual Machine
1. Open Oracle VirtualBox and click the New button.
2. Enter the VM Name: ubuntu-server-lab1, set Type to Linux, and Version to Ubuntu (64-bit).
   - Rationale: Explicitly defining the guest OS type allows VirtualBox to apply optimal default templates, such as proper kernel parameters and paravirtualization drivers tailored for Ubuntu.
3. Allocate 2048 MB (2 GB) of RAM.
   - Rationale: Calculated directly from the host's 8 GB memory limit. Allocating 2 GB provides the guest OS with sufficient working memory for system services and compilation tasks, while leaving the remaining ~6 GB free for the Windows 11 host to operate without performance degradation.
4. Select Create a Virtual Hard Disk Now using VDI (VirtualBox Disk Image) format.
   - Rationale: VDI is the native container format optimized specifically for Oracle VirtualBox performance and snapshot management.
5. Choose Dynamically Allocated storage and set the size ceiling to 25 GB.
   - Rationale: Dynamic allocation ensures that the virtual disk only consumes actual physical storage space on the host SSD as data accumulates, rather than instantly reserving the full 25 GB. The 25 GB limit provides safe overhead for updates and logs without overwhelming the host drive.
## 3. System Parameters and Network Verification
After completing the installation and booting into the guest OS for the first time, log into the console and run the following command-line verification tools:

1. Verify Memory Allocation: Run 'free -h'. Rationale & Verification: Confirms that the hypervisor correctly provisioned the target 2 GB RAM (~1.6 GiB usable memory visible in the output).
2. Verify Storage Layout and Disk Size: Run 'df -h' and 'lsblk'. Rationale and Verification: Checks root filesystem allocation to verify that the 25 GB virtual storage disk (sda) is correctly partitioned and mounted.
3. Verify Network and Internet Connectivity: Run 'ip addr' and 'ping -c 3 8.8.8.8'. Rationale & Verification: Confirms that the virtual network interface (enp0s3) successfully obtained an IP address via DHCP and verifies external internet connectivity through active packet exchange with 0% packet loss.
