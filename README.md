# CTF Note  

## 📖 Description  
Personal knowledge base for CTF — mainly focusing on **binary exploitation** and **system-level challenges**.  
This is organized like a mini-wiki so I can quickly find references, snippets, and challenge notes.  

---

## 📚 Table of Contents  

### 🔧 Setup Tools  
- [Pwntools](setup_tools/pwntools.md)  
- [GDB (gef/pwndbg/peda)](setup_tools/gdb.md)  
- [tmux](setup_tools/tmux.md)  
- [Docker & Environments](setup_tools/docker.md)  

### 🛠 Binary Exploitation  
- [Format String](binary_exploitation/format_string/README.md)  
- [Heap](binary_exploitation/heap/README.md)  
- [Shellcode](binary_exploitation/shellcode/README.md)  
- [TLS (Thread Local Storage)](binary_exploitation/tls/README.md)  

### 💡 Tips & Tricks  
Reusable snippets, shortcuts, and common patterns.  
- [Leak libc](tips/leak_libc.md)  
- [ROP tricks](tips/rop_tricks.md)  
- [Syscall notes](tips/syscall_notes.md)  
- [Bypass ASLR](tips/bypass_aslr.md)  

### 🏗 Architectures  
- [ARM](architectures/arm/README.md)  
- [RISC-V](architectures/riscv/README.md)  
- (add more: x86, MIPS...)  

### 📂 Challenges  
- [AmateursCTF 2024 - baby-sandbox](challenges/2024-AmateursCTF/shellcode-sandbox.md)  
- [DownUnderCTF 2024 - faulty-kernel](challenges/2024-DownUnderCTF/faulty-kernel.md)  
- [DownUnderCTF 2024 - pac-shell](challenges/2024-DownUnderCTF/pac-shell.md)  

### 🔗 References  
- [nobodyisnobody](https://github.com/nobodyisnobody/)  
- [welchbj’s notes](https://github.com/welchbj/ctf/blob/master/docs/binary-exploitation.md)  

---

## 🧩 Notes  
- Challenges are stored in `/challenges/<YEAR>-<CTFName>/<challenge>.md`  
- Each challenge note should include:  
  - Short description  
  - Exploit strategy  
  - Interesting takeaways  
  - Tags (for indexing later)  

## 🚀 Goal  
This repo is both a **personal knowledge base** and a **quick reference** during CTFs, helping reduce time spent re-Googling common tricks and focus on solving challenges.  