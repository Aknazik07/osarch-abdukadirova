## Three-Tool Comparison & Where They Disagreed

### Setup and Observed Tools
- **htop (evidence/htop.png):** Run inside the Ubuntu 64-bit guest virtual machine (aknazik@aknazik-VMware-Virtual-Platform, 3.2Gi guest RAM, 3.3Gi swap) running under VMware Workstation.
- **Windows Task Manager (evidence/task-manager.png):** Run on the Windows 11 host system (aknazik), showing host OS processes, CPU/memory/disk/network utilization, and background/Windows processes.
- **Process Explorer (evidence/process-explorer.png):** Run on the Windows 11 host system (aknazik), providing a hierarchical parent–child process tree, detailed memory columns, and deep inspection of open handles and loaded DLLs.

### How They Inspect a Process (PID, Parent, Memory & Handles/FDs)
- PID and Parent Relationship: Each tool exposes process identity and hierarchy differently. htop displays Linux PID and can display PPID / tree view (F5 / tree mode) for tasks inside the Ubuntu guest. Windows Task Manager groups processes into categories (Apps, Background processes, Windows processes) with less emphasis on raw parent–child lineage, whereas Process Explorer explicitly renders parent–child indentation and process ancestry on the Windows host.
- Memory Figures: In htop (Linux), memory accounting distinguishes used memory, free memory, and reclaimable buff/cache / available memory alongside swap. In Windows Task Manager and Process Explorer, memory is reported using Windows concepts such as Working Set / memory usage, private/committed memory, and overall host RAM commit/usage.
- Open Handles verses File Descriptors: Linux tracks open files, sockets, and pipes per process as file descriptors (FDs) (visible via /proc/<PID>/fd or lsof, rather than as a default column in htop), whereas Windows tracks kernel object references (files, registry keys, mutexes, events, sections) as handles, which Process Explorer directly inspects and lists in its lower handle/DLL pane.

### Where They Agreed
- Normal Baseline Behavior: All three views reflect a system operating under normal conditions without runaway CPU saturation or memory exhaustion during baseline monitoring.
- Separation of System vs. User Activity: Each tool separates OS/system/background services from active user-facing sessions and applications, making it possible to distinguish routine system overhead from user workloads.

### Where They Disagreed or Used Different Names for the Same Concepts
- Guest VM Scope vs. Host OS Scope: The biggest difference is boundary/scope: htop only sees processes and memory allocated to the Ubuntu guest VM, whereas Task Manager and Process Explorer observe the Windows 11 host—including VMware Workstation itself (vmware-vmx.exe / VMware processes) alongside native Windows processes. Because the guest VM is a subset of host resources, total RAM, CPU load, and process lists are not directly 1:1 comparable without accounting for virtualization overhead.
- Different Terminology for Similar Concepts:
  - *Open resources:* File descriptors (FDs) in Linux/Ubuntu vs. Handles in Windows/Process Explorer.
  - *Memory metrics:* Linux used / free / buff/cache / available / Swap in htop vs. Windows memory/working-set/private/commit metrics in Task Manager and Process Explorer.
  - *Process hierarchy:* Linux PID / PPID / tree view in htop vs. Windows process groups in Task Manager and indented parent–child tree in Process Explorer.
- Detail Level and Capture Timing: Process Explorer exposes much deeper per-process internals (handles, DLLs, detailed process tree) than standard Task Manager, while htop is a terminal-based Linux monitor; in addition, the screenshots were captured at different moments across the guest and host environments, causing minor point-in-time differences in live counters.
