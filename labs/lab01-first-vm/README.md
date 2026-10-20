Lab1-virtual machine

For this laboratory work, I set up a virtual machine named ubuntu-server-lab1 using Oracle VM VirtualBox and installed Ubuntu Server 25.04 (64-bit).
Resource Allocation Justification
When configuring the virtual machine, I allocated 2048 MB (2 GB) of RAM to it. I chose this specific amount because Ubuntu Server runs entirely in a command-line interface without a heavy graphical desktop environment. Because there is no GUI consuming memory in the background, 2 GB is more than sufficient for running terminal commands, updating packages, and practicing basic Linux administration. At the same time, this allocation leaves plenty of free RAM for my Windows host laptop, ensuring that the system remains stable and responsive while running both systems simultaneously.
Summary of Lab Steps
Before making any core configuration changes, I created a clean baseline snapshot named clean-install. After saving this state, I deliberately broke the system configuration by removing the hostname file to simulate a critical error and verified that the issue persisted. Finally, I performed a rollback operation back to the clean-install snapshot, which successfully restored the virtual machine to its original working state and completely removed all changes.
