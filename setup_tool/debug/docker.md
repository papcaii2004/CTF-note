# Debugging Challenges with Docker

## 📖 Overview
Many CTF challenges ship as Docker containers.  
The cleanest way to debug is to run the binary inside the container with **gdbserver**, and attach from your host with `gdb` (or `gdb-multiarch` for other architectures).

---

## 🛠 Prerequisites
- Docker installed on your host machine
- `gdb` / `gdb-multiarch` installed on your host
- `gdbserver` installed inside the container (often already included, or else we should modify the `Dockerfile`)

---

## 🚀 Setup Steps

### 1. Start the container with debug permissions
```bash
docker run -it --rm -p 1234:1234 --cap-add=SYS_PTRACE --security-opt seccomp=unconfined chall-image
```

### 2. Inside container: run binary with gdbserver
```bash
gdbserver 0.0.0.0:1234 ./vuln
```
This will start the binary paused until you connect.

### 3. On host: attach with gdb
```bash
gdb ./vuln
(gdb) target remote localhost:1234
```
Now you can use all normal GDB commands: breakpoints, memory inspection, stepping, etc.

## 📌 Notes

- Always add --cap-add=SYS_PTRACE or debugging won’t work.
- For foreign architectures (ARM, MIPS, etc.) use:
```bash
gdb-multiarch ./vuln
(gdb) target remote localhost:1234
```