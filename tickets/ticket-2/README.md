# Office Workstation Specification (ticket-2)

## 1. Executive Summary & Role Profiles
We designed four differentiated office workstations instead of buying four identical PCs so budget goes where real workloads demand it:
- **Accountant (accountant)**: spreadsheets, accounting software, browser tabs, integrated graphics (Intel Core i3-14100), 16 GB DDR4 (2 x 8 GB), 1 TB NVMe SSD, Deepcool MATREXX 30, Deepcool PF450, 27" monitor.
- **Sales (sales)**: CRM in browser, 30–40 tabs, spreadsheets, video calls, integrated graphics (AMD Ryzen 5 5600G), 32 GB DDR4 (2 x 16 GB), 1 TB NVMe SSD, Deepcool MATREXX 30, Deepcool PF500, 24" Full HD monitor.
- **Designer (designer)**: visual/UI/graphic design workloads with dedicated GPU (GeForce RTX 4060), Intel Core i5-12400F, 32 GB DDR4 (2 x 16 GB), 1 TB NVMe SSD, Deepcool CC360, Deepcool PK650D, ASUS ProArt Display PA248QV.
- **Web Developer (web developer)**: local development environments, editors or containers, multitasking (Intel Core i5-14400), 32 GB DDR5, 1 TB NVMe SSD, Deepcool CC360, Deepcool PK550D, 27" QHD monitor.

## 2. Workloads, Bottlenecks & Key Trade-offs
- Memory & Storage vs. CPU/GPU: For browser-heavy and multitasking roles like sales and web developer, RAM capacity and fast NVMe storage prevent slowdowns and swapping under peak load, while accountant and sales do not need a dedicated GPU.
- Designer GPU & Display: Only designer gets a discrete GeForce RTX 4060 and a ProArt display because visual/design tasks benefit directly from GPU acceleration and color accuracy.
- Compatibility & BIOS Notes: All builds are checked in PCPartPicker (evidence/pcpartpicker-links.md). Any BIOS version warnings on motherboard or CPU pairings are documented as potential firmware update checks rather than physical blockers.

## 3. Budget, OS Licences & Kazakhstan Vendor Quotes
- Itemized costs are tracked in KZT in budget.csv with exact models, vendor sources (supporting delivery/availability in Kazakhstan), and verification dates, backed by evidence in evidence/vendor-quotes/.
- Monitors and operating system licences are explicitly included in the budget plan rather than omitted from totals.
- Total budget across all four roles: **[INSERT TOTAL KZT FROM budget.csv]** (see budget.csv for per-role breakdowns).

## 4. Evidence & Verification Links
- PCPartPicker build lists: evidence/pcpartpicker-links.md (accountant, sales, designer, web developer).
- Vendor price quotes & dates (KZT): evidence/vendor-quotes/.
- Detailed build reasoning: builds.md and budget.csv.

## 5. Answers to the Three Report Questions

### 1. Which machine will you upgrade first, eighteen months from now, and why?
We will upgrade the **web developer** workstation first in 18 months (or add capacity/components there first if local dev stacks grow). Development environments, local databases, containers, and browser/IDE workloads scale up fastest in memory and storage demands over a 1.5-year project cycle, whereas accountant and sales have stable office/CRM workloads that age more slowly.

### 2. Price the same four as pre-built machines from a vendor. What does the company gain and lose?
Comparing custom/component-specified builds against four pre-built vendor machines highlights a clear trade-off:
- What the company gains with pre-built vendor machines: single-vendor warranty/SLA, faster replacement or on-site/service-center support, less assembly or rocurement overhead, and predictable business support terms.
- What the company loses with pre-built vendor machines: higher unit cost for equivalent specs, rigid configurations (often overpaying for features a role does not need or getting weaker RAM/SSD/PSU parts in a given price tier), and less exact control over role-specific trade-offs.
### 3. One of these four will complain about performance within a month. Who, and about what?
If anyone complains within the first month, it is most likely the **designer (or web developer** under heavy concurrent loads):
- For **designer**, complaints would center on heavy multi-layer or high-resolution assets, rendering/export times, or VRAM or display bottlenecks if project files grow larger than expected.
- For **web developer**, complaints would center on heavy local containers or builds/emulators saturating RAM or CPU burst threads during peak compilation or multitasking.

