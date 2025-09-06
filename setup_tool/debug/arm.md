# ARM / AArch64 Debugging Setup

## 📖 Overview
When dealing with challenges in non-x86 architectures (ARM, AArch64, MIPS, etc.), we need an emulator and toolchain to run and debug the binaries.  
For ARM/AArch64, **QEMU** is the most common choice.

This guide assumes **Ubuntu 22.04 LTS** as the host environment.

---

## ⚙️ Installation

Install QEMU, compilers, and multiarch gdb:

```bash
sudo apt update
sudo apt install -y qemu-user \
    gcc-10-aarch64-linux-gnu \
    gcc-arm-none-eabi \
    gdb-multiarch
```

## 🚀 Usage

### Compiling C to ARM64 Binaries

Use the cross-compiler to build statically linked binaries:

```bash
aarch64-linux-gnu-gcc-10 -static hello.c -o hello
```

### Running ARM64 Binaries

```bash
qemu-aarch64 ./hello
```

### 🐛 Debugging ARM Binaries

You can run QEMU in “debug server” mode and connect via GDB:

```bash
# Start QEMU with gdb stub
qemu-aarch64 -g 9999 ./hello
```

```bash
# In another terminal: connect with gdb-multiarch
gdb-multiarch -q ./hello

Reading symbols from ./hello...
(No debugging symbols found in ./hello)
(gdb) target remote :9999
Remote debugging using :9999
0x00000000004000b0 in _start ()
```

## 📌 Notes

- `gdb-multiarch` supports debugging binaries for different CPU architectures (ARM, AArch64, MIPS, RISC-V, etc.).
- For dynamic binaries (non-static), make sure you also have the right qemu-user-static and foreign libc available.
- You can combine this setup with Docker if the challenge runs inside a container.