# Environment Setup
The first step towards making your own OS is to setup the environment for developing a RISC-V kernel.

- If you're on Linux, this is pretty simple as most distros package both QEMU and RISC-V GNU toolchains.
- If you're on MacOS, you can install QEMU and the toolchain through Homebrew.
- If you're on Windows, things get a bit more complicated. If you can, I highly recommend using WSL for this project as it gives you a complete Linux environment on windows. 
If that's not possible, I recommend you use MSYS2 to get a Unix-like environment (that still runs normal Windows binaries) and then install a RISC-V toolchain + QEMU from there.
