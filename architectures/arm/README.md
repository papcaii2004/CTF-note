# What I know about Arm architecture

In this context I will work with `AArch64`(ARM64)  

:bangbang: About how to run and compile `AArch64` binary on `x86_64` machine you can refer to my qemu section in [Setup](https://github.com/papcaii/CTF-note/tree/main/setup_tool) dir 

## Assembly

Well always start with assembly, right

#### Register Naming
The aarch64 registers are named:

- r0 through r30 - to refer generally to the registers
- x0 through x30 - for 64-bit-wide access (same registers)
- w0 through w30 - for 32-bit-wide access (same registers - upper 32 bits are either cleared on load or sign-extended (set to the value of the most significant bit of the loaded value)).

#### Calling Convention
Usage during syscall/function call:

- r0-r7 are used for arguments and return values; additional arguments are on the stack
- For syscalls, the syscall number is in r8

- r9-r15 are for temporary values (may get trampled)

- r16-r18 are used for intra-procedure-call and platform values (avoid)
- The called routine is expected to preserve r19-- r28 *** These registers are generally safe to use in your program.

- r29 and r30 are used as the frame register and link register (avoid)

#### Instruction
We can refer to some of these useful docs/posts:
[Scott Wolchok](https://wolchok.org/posts/how-to-read-arm64-assembly-language/)

## Mitigation
There are still some mitigations similar to `x86_64` like
- RELRO
- Canary
- NX
- PIE/ASLR  

But there are something new

#### PAC (Pointer Authentication Code)
In `AArch64`, PAC (Pointer Authentication Code) is a security feature that helps protect against certain types of attacks, such as return-oriented programming (ROP) and jump-oriented programming (JOP)

![image](https://github.com/user-attachments/assets/f28e84e1-3858-4fc5-834d-407f3fbad3b2)

The PAC is placed in the unused high bits of a 'normal' pointer

It works by adding a cryptographic signature to pointers, ensuring that they haven't been tampered with. When the pointer is later used, the system verifies the signature, and if it doesn't match, the pointer is considered invalid, preventing unauthorized code execution

## Reference
[Azure](https://azeria-labs.com/writing-arm-assembly-part-1/)
