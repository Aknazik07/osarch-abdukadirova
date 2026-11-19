- Host Disk reserved: keep at least 15–20 GB free on the host drive so Windows 11 and temporary/swap files do not fill the disk
- CPU arithmetic:
  - Host total cores: <N> | Ubuntu Server: 2 vCPU | Windows 11: 2 vCPU | Total vCPUs assigned: 4 vCPU (<4 <= N ? "Within host core count" : "Overcommitted vCPUs (4 > N)" — adjust to <N> from Task 1).
- Memory arithmetic:
  - Total host RAM: 8192 MB
  - Ubuntu Server (2048 MB) + Windows 11 (3072 MB) = 5120 MB (5 GB)
  - Remaining host RAM: 8192 - 5120 = 3072 MB (3 GB) — matches the 3 GB host reserve assumption.
- Disk arithmetic:
  - Host free space (Task 1): <F> GB
  - Allocated virtual disks (dynamically allocated): 25 GB (Ubuntu Server) + 40 GB (Windows 11) = 65 GB provisioned (<actual_initial_size_GB> GB initially used on disk).
  - Remaining free space after provisioning/growth: <F - 65> GB (if <F < 85>, reduce virtual disk size or run one guest at a time so host free space stays safe).

### 3. Justification
- Why each choice was made:
  - **Ubuntu Server (2 vCPU, 2048 MB RAM, 25 GB dynamic disk):** A server install without a heavy desktop environment runs cleanly on 2 GB RAM and 2 vCPUs while leaving enough memory for the Windows 11 guest and host OS. Dynamic allocation avoids reserving 25 GB upfront on disk.
  - **Windows 11 (2 vCPU, 3072 MB RAM, 40 GB dynamic disk):** Windows 11 needs more memory and disk space than Ubuntu Server; 3072 MB is the closest allocation on an 8 GB host while preserving 3072 MB for the host OS.
  - **Network mode (NAT):** Gives both guests internet access and lets the host reach Ubuntu Server over ssh (via forwarded port or NAT interface) while keeping the test lab isolated from external LAN hosts.
- Trade-offs / anything set below an ideal minimum:
  - Running both guests simultaneously on 8 GB total host RAM leaves 3 GB for Windows 11 on the host and gives the Windows 11 guest 3 GB (3072 MB), which is tight for heavy multitasking inside the Windows 11 guest. If the host cannot comfortably run both at once with your Task 1 figures, the closest working alternative is running one guest at a time (giving Windows 11 4096 MB when run alone, or Ubuntu Server 2048–4096 MB when run alone) or reducing Windows 11 guest RAM to 2048–3072 MB only for light testing.

### 4. Verification Plan
*(State where each command is run—Ubuntu guest, Windows 11 guest, or Windows host—and the expected output proving the plan worked.)*

1. Verify Ubuntu Server resources (run inside Ubuntu Server guest):
   - Command: nproc && free -h && df -h /
   - Expected output: 2 processors shown by nproc; ~2.0 Gi total memory in free -h; root filesystem capacity around 25G in df -h /.
2. Verify Windows 11 guest resources (run inside Windows 11 guest PowerShell/Command Prompt):
   - Command: systeminfo | findstr /B /C:"OS Name" /C:"Total Physical Memory" and (Get-CimInstance Win32_Processor).NumberOfLogicalProcessors
   - Expected output: Total Physical Memory around 3,072 MB (~3 GB) and 2 logical processors.
3. Verify SSH reachability from host to Ubuntu Server (run on Windows host):
   - Command: ssh -p <ssh_port> <ubuntu_user>@<ubuntu_or_nat_host_ip> "hostname && whoami"
   - Expected output: Connects over SSH (authenticates via key or password) and prints the Ubuntu Server hostname and <ubuntu_user>.
4. Verify internet access from Ubuntu Server guest (run inside Ubuntu Server guest):
   - Command: ping -c 3 1.1.1.1 && curl -I -s --max-time 5 https://ubuntu.com | head -n 1
   - Expected output: 3 received, 0% packet loss from ping and an HTTP status line (e.g., HTTP/2 200 or HTTP/1.1 ...) from curl.
5. Verify host remains usable (run on Windows host):
   - Check Task Manager (Ctrl + Shift + Esc) / free disk space (Get-PSDrive C) while both VMs are running: host stays responsive without freezing, and free disk space remains above the host reserve threshold.
