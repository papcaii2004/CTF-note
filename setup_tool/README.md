# Setup your computer with neccesary tool

Note: This setup was used for Ubuntu 22.04 LTS

## Qemu

### Usage  
When we have to deal with binaries from different architecture (like arm, arm64 (aarch64), mips, ...), we need an emulator to run and debug these binaries. 
In my opinion, Qemu is a one of the best choices.

### Installation  
```bash
sudo apt install qemu-user
sudo apt-get install gcc-10-aarch64-linux-gnu
sudo apt install gcc-arm-none-eabi
sudo apt install gdb-multiarch
```

### Compiling C to ARM64 Binaries
```bash
aarch64-linux-gnu-gcc-10 -static hello.c -o hello
```

### Runing ARM64 Binaries
```bash
qemu-aarch64 ./hello
```

### Disassembling ARM64 Binaries
```bash
aarch64-linux-gnu-objdump -D hello
```

### Debugging ARM Binaries
```
$ qemu-aarch64 -g 9999 ./hello
$ gdb-multiarch -q ./hello
Reading symbols from ./hello...
(No debugging symbols found in ./hello)
(gdb) target remote :9999
Remote debugging using :9999
0x00000000004000b0 in _start ()
(gdb) set disassemble-next-line on
```
