---
layout: default
title: Stack Protection Techniques
---

<h2>{{ page.title }}</h2>
0x0 checksec
---

```
root@kali:~/Documents/_rop# checksec level2
[!] Pwntools does not support 32-bit Python.  Use a 64-bit release.
[*] '/root/Documents/_rop/level2'
    Arch:     i386-32-little
    RELRO:    Partial RELRO
    Stack:    No canary found
    NX:       NX enabled
    PIE:      No PIE (0x8048000)
```


0x1 DEP / NX (No-eXecute)
---
1. If DEP / NX is on, the shellcode is no longer executable on the Stack. 
2. This protection tech can be set in the meantime of COMPILATION.
3. To switch off: 
```
$ gcc -z execstack helloworld.c
```

0x2 ALSR / PIE 
---
1. If ALSR is on, every time executing the program, the address of Labc, stack and heap will be randomized, the address of the program would not be randomized.
Check ALSR:
```
cat /proc/sys/kernel/randomize_va_space
```

Switch off ALSR:
```
sudo echo 0 > /proc/sys/kernel/randomize_va_space
```
2. PIE (position-independent executables): Commonly the system ALSR keeps on, the program can switched off the PIE if the programer dose not want extra system overhead.

0x3 RELRO
---
1. To protect GOT attack. 

2. Partial RELRO

compiler command line: gcc -Wl,-z,relro

the ELF sections are reordered so that the ELF internal data sections (.got, .dtors, etc.) precede the program's data sections (.data and .bss)

non-PLT GOT is read-only

GOT is still writeable

3. Full RELRO

compiler command line: gcc -Wl,-z,relro,-z,now

supports all the features of partial RELRO

bonus: the entire GOT is also (re)mapped as read-only

0x4 Stack Protector / Canary / GS (Windows)
---
1. When a return address is stored in a stack frame, a CANARY value is written just before it. Any attempt to rewrite the address using buffer overflow will result in the canary being rewritten and an overflow will be detected.
2. This protection tech can be set in the meantime of COMPILATION.
3. To switch off: 
```
$ gcc -fno-stack-protector helloworld.c
```
4. gcc 4.2 and later support switching on the protection:
```
$ gcc -fstack-protector helloworld.c
$ gcc -fstack-protector-all helloworld.c
```
5. gcc 4.9 and later support switching on the protection:
```
$ gcc -fstack-protector-strong helloworld.c
```
6. Type of Canaries

Terminator canaries, Random canaries, Random XOR canaries.

0x5 FORTIFY_SOURCE
---
Since the compiler can know the size of a buffer with a known buffer size, functions that operate on the buffer can make sure the buffer will not overflow. Basicly "FORTIFY_SOURCE" would add instructions (optimization) to detect if the length of the buffer.



