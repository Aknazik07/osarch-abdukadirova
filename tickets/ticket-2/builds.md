All four builds meet the mandatory baseline per machine: at least 16 GB RAM, at least 1 TB SSD, a licensed operating system, and one monitor, priced in KZT from vendors delivering to Kazakhstan with a recorded price date.

---

### Build 1 — Accountant (accountant)
* Load: 1C accounting software, large Excel workbooks (tens of thousands of rows), browser with bank portals and tax/invoicing web apps (10–15 tabs), PDF documents, ~8 hours/day.
* Bottleneck: Single-core CPU speed and monitor workspace/resolution. Legacy accounting workflows and heavy spreadsheet formulas depend heavily on single-thread responsiveness, while cramped screens force constant horizontal/vertical scrolling and eye strain.
* Trade-off: Skipped a discrete GPU (relying on integrated graphics) and started with 16 GB RAM (minimum required) instead of 32 GB upfront, putting budget into a fast single-core processor (Intel Core i3-14100) and a 27-inch QHD (2560×1440) monitor for wide spreadsheets.
* Total: <SUM_ACCOUNTANT_KZT> KZT (budget.csv, rows <START_ROW>–<END_ROW>)

---

### Build 2 — Sales (sales)
* Load: CRM in a browser, 30–40 tabs, Excel, four hours of video calls a day, sometimes all at once.
* Bottleneck: Memory, not CPU. Chrome with forty tabs plus a video call is around 11–12 GB. On 8 GB (or tight memory headroom) the machine starts swapping in the middle of a customer call.
* Trade-off: Took a Ryzen 5 5600G with integrated graphics instead of a higher-tier CPU / discrete GPU and spent the saved money on 32 GB RAM instead of 16 GB. The CPU has plenty of headroom for this role; memory capacity is the priority.
* Total: <SUM_SALES_KZT> KZT (budget.csv, rows <START_ROW>–<END_ROW>)

---

### Build 3 — Web Developer (web_dev)
* Load: VS Code / IDE, local dev servers, Docker containers (database, backend, cache), local frontend/backend builds, and browser DevTools across ~6–8 active hours/day.
* Bottleneck: Multi-core CPU, memory, and SSD throughput/latency. Running containers, compilers, and bundlers in parallel saturates CPU cores and RAM, while large dependency trees and container layers stress storage speed.
* Trade-off: Omitted a discrete GPU (web development and local container workloads do not need a dedicated graphics card) and allocated budget to a 10-core/16-thread Intel Core i5-14400, 32 GB DDR5, a fast PCIe 4.0 NVMe SSD (Kingston KC3000 1TB), and a 27-inch QHD display to keep editor panes and browser previews side by side.
* Total: <SUM_WEB_DEV_KZT> KZT (budget.csv, rows <START_ROW>–<END_ROW>)

---

### Build 4 — Designer (designer)
* Load: Adobe Photoshop (multi-layer files up to ~1 GB), Illustrator, Figma, light motion/compositing or rendering tasks, and browser reference boards throughout the workday.
* Bottleneck: GPU acceleration, monitor colour accuracy, and memory capacity. Canvas compositing, filters/effects, and exports slow down without a capable GPU, while inaccurate displays risk colour mismatch across deliverables.
* Trade-off: Used an Intel Core i5-12400F (no need for integrated graphics or an expensive i7 tier) and 32 GB DDR4 instead of DDR5 so budget could go toward a discrete NVIDIA RTX 4060 8GB GPU and a colour-accurate ASUS ProArt monitor.
* Total: <SUM_DESIGNER_KZT> KZT (budget.csv, rows <START_ROW>–<END_ROW>)
