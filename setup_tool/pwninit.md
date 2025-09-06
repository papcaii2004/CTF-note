# pwninit

## What is it?  
[pwninit](https://github.com/io12/pwninit) is a tool to quickly generate an exploit template and patch binaries with the provided libc.  
It saves a lot of boilerplate setup when starting a new pwn challenge.

---

## Installation  

```bash
# Clone & install
git clone https://github.com/io12/pwninit
cd pwninit
cargo install --path .
```

Make sure ~/.cargo/bin is in your $PATH.

## 🚀 Usage

### Basic

```bash
pwninit
```

This will:

- Automatically patch the binary with the given libc.
- Create a solve.py (We can modify its template).
- Create ld.so symlink if necessary.

## Template

### Default `solve.py`

```python
#!/usr/bin/python3
from pwn import *
import os

# Load binary (set by pwninit)
e = context.binary = ELF("./vuln", checksec=False)

# pwntools defaults
context.terminal = ["tmux", "splitw", "-h", "-p", "60"]  # adjust to your terminal
context.log_level = "debug" if os.getenv("DEBUG") else "info"

def start():
    """Start the exploit based on args/env"""
    if args.REMOTE:
        HOST = os.getenv("HOST", "0.0.0.0")
        PORT = int(os.getenv("PORT", "8888"))
        return remote(HOST, PORT)

    elif args.GDBREMOTE:
        HOST = os.getenv("GDB_HOST", "127.0.0.1")
        PORT = int(os.getenv("GDB_PORT", "1234"))
        gdb_cmd = f"target remote {HOST}:{PORT}"
        return gdb.debug([e.path], gdbscript=gdb_cmd)

    elif args.LOCAL:
        return process([e.path])

    else:
        return gdb.debug([e.path], gdbscript=gdbscript)

gdbscript = """
break main
continue
"""

p = start()
p.interactive()
```


### For challenge need qemu

- Replace the `start()` function with:
```python
def start():
    """Run exploit under qemu-user"""
    qemu = os.getenv("QEMU", "qemu-aarch64")  # default: ARM64
    if args.REMOTE:
        HOST = os.getenv("HOST", "0.0.0.0")
        PORT = int(os.getenv("PORT", "8888"))
        return remote(HOST, PORT)
    elif args.LOCAL:
        return process([qemu, e.path])
    else:
        return process([qemu, "-g", "1234", e.path])  # default qemu debug
```