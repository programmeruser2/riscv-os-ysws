# The Machine
Currently, there is no emulator for any of the JH7110 SOC-based boards (which is what the board we will ship to you), so we will stick to QEMU's virt machine to keep things simple.

The virt machine is basically a fake machine the QEMU authors made up that is mainly used to run virtualized OSes. So there is no real-world board that is based on the virt machine, it's 100% virtualized. 

QEMU simulates an NS16550-based UART (a serial device that we will use to implement a simple terminal interface), but we will instead use something called OpenSBI to interact with the terminal interface.

OpenSBI is kind of like a universal BIOS for RISC-V, since it handles some basic booting functions and also provides some functions for interfacing with hardware that can be accessed through `ecall` (basically syscalls). 
Since these interface functions are universal across hardware, we will use OpenSBI functions instead of writing drivers for the specific virt hardware to make our OS more portable.

# So how does RISC-V boot?
Firstly, QEMU jumps to the OpenSBI firmware, which does some initialization stuff.

Depending on the type of OpenSBI firmware, it may jump to a fixed location or a dynamic location determined by the ELF metadata. 
To keep things simple we will just use the default, which is the dynamic version of OpenSBI. 
However, we will need to place our kernel after the OpenSBI firmware.

# How do I understand RISC-V?
If you haven't read "Putting the You in CPU", I highly recommend you to because it does an excellent job of explaining computer architecture from the ground up.

For specific RISC-V ISA information, most of it can be found in the manual: https://github.com/riscv/riscv-isa-manual. 
There is also some other miscellaneous specifications that can be found in https://github.com/riscv.

# A quick introduction 

RISC-V is a RISC architecture. Which means that it basically has many simple instructions instead of large, complex instructions (CISC). 

This means that it takes more instructions to express the same operation in RISC-V compared to a CISC architecture.

This may seem negative, but it allows CPUs to perform better, especially in resource-constrained environments, and is much simpler for beginners.

I chose RISC-V for this YSWS specifically because it is a modern CPU architecture that has relatively little cruft compared to other architectures.

Before embarking on the OS dev journey, I recommend you read up on RISC-V assembly: https://riscv-programming.org/. 
If you already know an assembly language like x86 or ARM, RISC-V assembly should be similar and just reading over the manual should suffice.
Otherwise, I highly recommend you to understand how RISC-V assembly works so you get a deeper understanding of it.

In this guide, we will get a simple kernel to boot, get I/O working, setup interrupts, and give you the ingredients to implement an advanced feature of your choice.

Good luck!
