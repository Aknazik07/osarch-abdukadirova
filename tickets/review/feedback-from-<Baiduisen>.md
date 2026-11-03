# Feedback on <Baiduisen>'s BUILD.md
Reviewer: <Aimaral Baiduisen>
Commit reviewed: <https://github.com/a8615/osarch-baiduisen/tree/185a333dc35fed3ceaef49bddbbe01c2b4fe7d49/tickets/ticket1-vm-build-doc/review>
Hypervisor I used: Oracle VirtualBox version 7.x

## First step where I got stuck
Step number: Step 1, Item 3 (RAM allocation subsection)
What the step says: "Allocate 2048 MB (2 GB) of RAM."
What I did: Opened the virtual machine settings in VirtualBox to specify the RAM size.
What happened / what I had to guess: In the VirtualBox interface, the slider or input field accepts values in megabytes, and although the text says 2048 MB, the slider in VirtualBox isn't always easy to drag to the exact megabyte on the first try — I had to manually type the number 2048 into the input field, as the guide didn't specify that typing the exact number manually is easier.
## Other places I hesitated
- Step 2, Item 2: The name ubuntu-server-lab1 is specified, but it wasn't clarified whether case sensitivity or hyphens affect subsequent steps (even though it's standard).

## Settings I would not have chosen without the document
- Using a dynamically allocated virtual disk size capped at 25 GB with the VDI format — the Rationale for each point was explained in great detail, which helped make this configuration consciously.

## One thing that worked well
- Excellent and very detailed structure with a Rationale section for each step. The verification commands (free -h, df -h, ip addr) in Section 3 are laid out very clearly.
