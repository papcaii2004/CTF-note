# CTF Note

## Description  
I will store some knowledge here for reference

## Some tips  
I know sth new

#### Format String
Urgg, I hate this, why people keep spamming these challenges !!! [FSB](FSB)

#### ARM
This is a lot of things so I will give it a directory for it [ARM](ARM)

### Leak libc  
Some weird challs that dont give us libc, so we have to find it ourself, here is a short script that will do it: 

```python
if not 'libc' in locals():
    try:
        import requests
        r = requests.post('https://libc.rip/api/find', json = {'symbols':{'puts':hex(puts)[-3:]}})
        libc_url = r.json()[0]['download_url']
        libc_file = libc_url.split('/')[-1:][0]
        if not os.path.exists(libc_file):
            log.info('getting: ' + libc_url)
            r = requests.get(libc_url, allow_redirects=True)
            open(libc_file,'wb').write(r.content)
    except:
        log.critical('get libc yourself!')
        sys.exit(0)
    libc = ELF(libc_file)

libc.address = puts - libc.sym.puts
log.info('libc.address: ' + hex(libc.address))
```

In above example, I test when I leak `puts` address

#### TLS
when a child thread is created, the TLS(Thread Local Storage) will be stored next to the new stack of the child thread like this  
![image](https://github.com/user-attachments/assets/5d34f127-589c-4cca-ba3e-95e89b63313e)  
this contains some useful information like master canary   
-> we can leak or overwrite this 

## Some good references

[nobodyisnobody](https://github.com/nobodyisnobody/): Various docs with huge amount of writeups  
[welchbj](https://github.com/welchbj/ctf/blob/master/docs/binary-exploitation.md): Some interesting notes and techniques

## Challenge Index

<details>
<summary><h3>Heap challenges</h3></summary>
<p>

</p>
</details>

<details>
<summary><h3>Shellcode</h3></summary>
<p>
  
***Amateurs CTF 2024*** --> [baby-sandbox](https://hyggehalcyon.gitbook.io/page/ctfs/2024/amateursctf)  
> Shellcode using `sysenter` to escape sandbox where syscall are forbidden
> 
> Using register `xmm` to deal with deleted register

</p>
</details>

<details>
<summary><h3>Linux Kernel</h3></summary>
<p>

***DownUnder CTF 2024*** --> [faulty-kernel](https://github.com/DownUnderCTF/Challenges_2024_Public/tree/main/pwn/faulty-kernel)
> An arm64-bin challenge, which allow us to read, write arbitrary address
> 
> Use arm-gadget to invoke call to `system(/bin/sh)`

</p>
</details>

<details>
<summary><h3>Different architecture</h3></summary>
<p>

***DownUnder CTF 2024*** --> [pac-shell](https://github.com/DownUnderCTF/Challenges_2024_Public/tree/main/pwn/pac-shell)
> An arm64-bin challenge, which allow us to read, write arbitrary address
> 
> Use arm-gadget to invoke call to `system(/bin/sh)`

</p>
</details>
