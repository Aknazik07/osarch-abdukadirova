1. 
* Model: Acer TravelMate Spin B3 (B311RN-31)
* Manual Link: [Acer TravelMate Spin B3 B311RN-31 PDF Document](https://manual-hub.com/manuals/acer-travelmate-spin-b3-b311rn-31-01-pdf-manual/)
## 2. Components

1. CPU and Heatsink (Processor Zone)
  * What: Motherboard CPU zone covered by a copper heatsink shield, housing the soldered processor.
  * Connects to: Power delivery circuits, internal buses, and system board architecture
  * Limits: CPU is permanently soldered (BGA) and non-upgradeable; passive cooling solution without a dedicated fan.

 2. M.2 SSD Slot / Storage
  * What: M.2 expansion slot containing a solid-state drive (Kingston 128GB)
  * Connects to: PCIe / SATA controller on the motherboard
  * Limits: Supports M.2 NVMe / SATA form factor (typically 2280 size key); fully upgradeable and replaceable.

 3. Wi-Fi Module
  * What: Wireless communication card for Wi-Fi and Bluetooth connectivity (M.2 2230 format)
  * Connects to: Small M.2 slot (A/E key) on the motherboard and internal antenna cables
  * Limits: Compatible with standard wireless card form factors; upgradeable.

 4. Main Battery
  * What: Rechargeable Li-ion battery pack, model Acer AP18C8K (3INPS/82/70), 11.25V, 4343 mAh / 48.85 Wh
  * Connects to: Dedicated multi-pin power connector on the system board
  * Limits: Removable and replaceable component designed for specific voltage and capacity thresholds

 5. I/O Ports and Daughterboard
  * What: Side-mounted input/output interface ports (USB, HDMI, audio jack, Ethernet RJ-45, DC-in)
  * Connects to: Main system board via flexible flat ribbon cables (FPC) and dedicated traces
  * Limits: Transfer speeds and electrical ratings are bound by controller specifications (e.g., USB 3.2 Gen 1 up to 5 Gbps)
  

## 5. The Upgrade Verdict

| Component | Manual says | OS says | Verdict |
| :--- | :--- | :--- | :--- |
| Memory | 8 GB soldered + 1 SO-DIMM slot, max 40 GB | 2 devices, 1 SO-DIMM, MaxCapacity 64 GB | Partly: One free slot, upgradeable up to 32/40 GB (manual limit takes precedence over firmware table limits). |
| Storage | 1 x M.2 2280, PCIe NVMe | BusType: NVMe | Yes: Fully upgradeable to any compatible 2280 NVMe drive. |
| CPU | Part of the system board | SocketDesignation: BGA1744 | No: Soldered directly to the motherboard, non-replaceable. |
## 8. The comparison table

| Fact | Windows | Linux (VM) |
| :--- | :--- | :--- |
| Logical CPUs | Get-CimInstance Win32_Processor -> NumberOfLogicalProcessors = 8 | lscpu -> CPU(s) = 8 (or VM allocation) |
| Total memory | Get-CimInstance Win32_ComputerSystem -> TotalPhysicalMemory = ~8 GB | free -h -> total ~ 7.6 GB |
| Disk interface | Get-PhysicalDisk -> BusType = NVMe | lsblk -> TRAN = nvme |

* Analysis: 
  * Naming differences: Windows queries rely on WMI/CIM classes and properties (such as Win32_Processor), whereas Linux utilizes command-line utilities and virtual filesystems (such as lscpu and free).
  * Values & Host vs VM: The hardware metrics match closely because they describe the underlying physical capabilities of the Acer TravelMate machine, though minor variations in total memory appear due to system reservations and hypervisor memory management.
