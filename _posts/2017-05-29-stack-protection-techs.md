---
layout: default
title: Stack Protection Techniques
---

<h2>{{ page.title }}</h2>


0x1 DEP / NX (No-eXecute)
---
1. If DEP / NX is on, the shellcode is no longer executable on the Stack. 
2. This protection tech can be set in the meantime of COMPILATION.
3. To switch off: 
```
gcc  -z execstack
```

0x2 Stack Protector / Canary / GS (Windows)
---
1. When a return address is stored in a stack frame, a CANARY value is written just before it. Any attempt to rewrite the address using buffer overflow will result in the canary being rewritten and an overflow will be detected.
2. This protection tech can be set in the meantime of COMPILATION.
3. To switch off: 
```
gcc -fno-stack-protector
```
4. gcc 4.2 and later support switching on the protection:
```
-fstack-protector 
-fstack-protector-all 
```
5. gcc 4.9 and later support switching on the protection:
```
-fstack-protector-strong
```
6. Type of Canaries
Terminator canaries, Random canaries, Random XOR canaries.

0x3 Stack Protector / Canary / GS (Windows)
---
