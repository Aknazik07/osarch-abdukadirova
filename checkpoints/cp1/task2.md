## 1. Both guests?
Running both Lab 1-2 guests at the same time on an 8 GB RAM host running Windows 11 Home in S mode is not practical if both require substantial memory alongside the host OS.
- Total host RAM: 8192 MB (8 GB)
- Host reserve for Windows 11 + hypervisor: ~3072 MB (3 GB)
- Remaining RAM for VMs: ~5120 MB (5 GB)
- If the combined RAM of the two Lab 1-2 guests plus host overhead exceeds 8192 MB (or leaves less than ~2-3 GB for Windows 11), running both simultaneously will cause heavy swapping, lag, or out-of-memory crashes.

## 2. Upgrade first
- *Priority:* RAM first, because memory overcommitment on an 8 GB system causes immediate slowdowns or VM crashes, followed by free disk space for VM images.
- *Upgradeability & fallback:* On many compact laptops (such as TravelMate Spin B3 models), RAM is soldered and cannot be upgraded. If nothing on the hardware can be upgraded, run one guest at a time instead of both together, keep Ubuntu Server lightweight without extra background apps, and close unused host programs before starting a VM.

---

# Task 2 — Plan and Justify

## Allocation
- *Host:* Windows 11 Home in S mode, 8192 MB (8 GB) RAM, <N> cores from Task 1, <F> GB free disk space from Task 1.
- *Ubuntu Server guest:* 2 vCPUs, 2048 MB (2 GB) RAM, 25 GB dynamically allocated disk, 1 NIC in NAT mode (with port forwarding or host-reachable NAT IP for SSH).
- *Windows 11 guest:* 2 vCPUs, 3072 MB (3 GB) RAM, 40 GB dynamically allocated disk, 1 NIC in NAT mode.

## Arithmetic
- *Host assumptions:* Reserve 3072 MB (3 GB) RAM for Windows 11 and VMware/hypervisor overhead, keep at least 15-20 GB free disk space on the host, and avoid starving host CPU threads.
- *CPU:* 2 vCPU (Ubuntu Server) + 2 vCPU (Windows 11) = 4 vCPUs total against <N> host cores from Task 1.
- *Memory:* 2048 MB (Ubuntu Server) + 3072 MB (Windows 11) = 5120 MB (5 GB) allocated to guests; 8192 MB - 5120 MB = 3072 MB (3 GB) left for the host.
- *Disk:* 25 GB + 40 GB = 65 GB dynamically allocated (initially takes only the actual guest disk footprint); <F - 65> GB remaining if fully grown against <F> GB free in Task 1.

## Justification
- *Ubuntu Server (2 vCPU, 2048 MB, 25 GB dynamic):* A server guest has no heavy GUI overhead, so 2 GB RAM and 2 vCPUs are enough for normal lab tasks while leaving memory for Windows 11 and the host. Dynamic disk allocation avoids wasting space before data is written.
- *Windows 11 guest (2 vCPU, 3072 MB, 40 GB dynamic):* Windows 11 needs more RAM and disk than Linux; 3072 MB is the closest allocation on an 8 GB host while keeping 3 GB free for the host OS.
- *NAT networking:* Gives both guests internet access and allows SSH from the host to Ubuntu Server while keeping lab traffic off the wider LAN.
- *Below-ideal trade-off:* 3072 MB RAM on the Windows 11 guest and running both guests together on 8 GB total RAM is tight for heavy multitasking. If both cannot run smoothly at once with Task 1 numbers, the closest working setup is running one guest at a time (e.g., 4096 MB RAM when running the Windows 11 guest alone).

## Verification Plan
1. *Ubuntu Server resources (inside Ubuntu Server guest):*
   nproc && free -h && df -h /
   Expected: 2 CPUs, ~2.0Gi total RAM, and ~25G root filesystem size.
2. *Windows 11 guest resources (inside Windows 11 guest):*
   systeminfo | findstr /B /C:"OS Name" /C:"Total Physical Memory" and (Get-CimInstance Win32_Processor).NumberOfLogicalProcessors
   Expected: ~3,072 MB total physical memory and 2 logical processors.
3. *SSH from host to Ubuntu Server (on Windows host):*
   ssh -p <port> <user>@<host_or_vm_ip> "hostname && whoami"
   Expected: Successful SSH login and output showing the Ubuntu Server hostname and username.
4. *Internet access from Ubuntu Server (inside Ubuntu Server guest):*
   ping -c 3 1.1.1.1 && curl -I -s --max-time 5 https://ubuntu.com…
