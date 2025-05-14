# The Machine
Currently, there is no emulator for any of the JH7110 SOC-based boards (which is what the board we will ship to you), so we will stick to QEMU's virt machine to keep things simple.

The virt machine is basically a fake machine the QEMU authors made up that is mainly used to run virtualized OSes. So there is no real-world board that is based on the virt machine, it's 100% virtualized. 

QEMU simulates an NS16550-based UART (a serial device that we will use to implement a simple terminal interface), but we will instead use something called OpenSBI to interact with the terminal interface.

OpenSBI is kind of like a universal BIOS for RISC-V, since it handles some basic booting functions and also provides some functions for interfacing with hardware that can be accessed through `ecall` (basically syscalls). 
Since these interface functions are universal across hardware, we will use OpenSBI functions instead of writing drivers for the specific virt hardware to make our OS more portable.

