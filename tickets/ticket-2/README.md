# Office Workstation Specification (ticket-2)

## 1. Executive Summary & Role Profiles
We specified four differentiated office workstations tailored to actual workloads instead of four identical builds:
- **Accountant (accountant — 445,538 KZT)**: Intel Core i3-14100, MSI PRO H610M-E DDR4, Kingston FURY Beast 16GB (2x8GB) DDR4 3200MHz, Kingston NV3 1TB M.2 NVMe, DeepCool PF450 450W, DeepCool MATREXX 30, Xiaomi Monitor A27Qi 27 QHD, and Microsoft Windows 11 Home 64-bit (integrated graphics).
- **Sales (sales — 531,900 KZT)**: AMD Ryzen 5 5600G, MSI B550M PRO-VDH WIFI, Kingston FURY Beast 32GB (2x16GB) DDR4 3200MHz, Kingston NV3 1TB M.2 NVMe, DeepCool PF500 500W, DeepCool MATREXX 30, LG 24MR400-B 23.8 FHD, and Microsoft Windows 11 Home 64-bit (integrated graphics).
- **Web Developer (web_dev — 647,270 KZT)**: Intel Core i5-14400, MSI PRO B760M-A WIFI DDR5, Kingston FURY Beast 32GB (2x16GB) DDR5 5600MHz, Kingston KC3000 1TB M.2 NVMe PCIe 4.0, DeepCool PK550D 550W, DeepCool CC360, Xiaomi Monitor A27Qi 27 QHD, and Microsoft Windows 11 Pro 64-bit (integrated graphics).
- **Designer (designer — 940,382 KZT)**: Intel Core i5-12400F, Palit GeForce RTX 4060 Dual OC 8GB, MSI PRO B760M-P DDR4, Kingston FURY Beast 32GB (2x16GB) DDR4 3200MHz, Samsung 980 PRO 1TB M.2 NVMe, DeepCool PK650D 650W, DeepCool CC360, ASUS ProArt Display PA248QV, and Microsoft Windows 11 Home 64-bit.

## 2. Workloads, Bottlenecks & Key Trade-offs
- RAM capacity for browser/multitasking workloads: High browser tab counts, CRM, spreadsheets, and local dev tools put pressure on memory capacity first; sales, web_dev, and designer use 32 GB (2x16GB), while accountant uses 16 GB (2x8GB).
- Discrete GPU allocation: Only designer includes a discrete GPU (Palit GeForce RTX 4060 Dual OC 8GB) and color-focused ASUS ProArt Display PA248QV for visual/design work, whereas accountant, sales, and web_dev rely on integrated graphics.
- Storage & platform choices: NVMe SSDs (Kingston NV3, Kingston KC3000, Samsung 980 PRO) are paired with role-appropriate DDR4 or DDR5 platforms, and PCPartPicker compatibility checks (including any BIOS notes) are documented in evidence/pcpartpicker-links.md.

## 3. Budget, OS Licences & Kazakhstan Vendor Quotes
- All component, monitor, and OS licence prices are recorded in KZT in budget.csv (verified 2026-11-26) with Kazakhstan vendor links (kaspi.kz / shop.kz) and mirrored in evidence/vendor-quotes/quotes.md.
- Per-role totals in budget.csv: accountant = 445,538 KZT, sales = 531,900 KZT, web_dev = 647,270 KZT, designer = 940,382 KZT.
- Total specification cost across all four roles: 2,565,090 KZT.

## 4. Evidence & Verification Links
- PCPartPicker build lists: evidence/pcpartpicker-links.md (accountant, sales, designer, web developer).
- **Vendor price quotes (KZT, checked 2026-11-26)**: evidence/vendor-quotes/quotes.md.
- Budget & build notes: budget.csv and builds.md.

## 5. Answers to the Three Report Questions

### 1. Which machine will you upgrade first, eighteen months from now, and why?
We will upgrade the **web_dev** workstation first in 18 months. Local development environments, containers, build pipelines, and browser/IDE tooling expand steadily in memory and storage requirements over time, whereas accountant and sales have more stable office and CRM workloads that change less aggressively.

### 2. Price the same four as pre-built machines from a vendor. What does the company gain and lose?
Buying four pre-built vendor machines instead of specifying individual components creates a clear trade-off:
- What the company gains: centralized vendor warranty/service coverage, potentially faster replacement or support terms, and less time spent coordinating individual parts.
- What the company loses: flexibility to match exact RAM/SSD/GPU/monitor specs to each role's bottleneck without overpaying for unused extras or accepting compromises in standard pre-built tiers, as well as direct control over component-level pricing in KZT.

### 3. One of these four will complain about performance within a month. Who, and about what?
Within the first month, the most likely to complain is **designer (or web_dev** under heavy peak multitasking):
- For **designer**, complaints would likely involve slow rendering/export/asset handling or memory/VRAM limits if project complexity or file sizes exceed expectations.
- For **web_dev**, complaints would likely center on heavy local containers, builds, or multitasking pushing RAM or CPU burst performance during peak workloads.

