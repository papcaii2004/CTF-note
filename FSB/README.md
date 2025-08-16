# Format String Bug

## Basic

For reminding, we know that the linux calling convention is 
`rdi -> rsi -> rdx -> rcx -> r8 -> r9 -> rsp -> rsp+8 -> ...`

### Read primitive

- With `%p` we can leak value at the registers or specific parameters on stack
- Like I mention above, the index of FSB is corresponding to the calling convention
- 0 is `rdi`, 1 is `rsi`, 2 is `rdx` and so on...
- So to leak value at {index} we can use `%{input}$p`
- For example, with `printf('%7$p')` we will have value at {rsp+8}

### Write primitive

## Technique

### Abusing `printf` FSB to overwrite `printf` return address 

#### References
- [FCSC2022](https://github.com/voydstack/FCSC2022/tree/main/pwn/formatage)
