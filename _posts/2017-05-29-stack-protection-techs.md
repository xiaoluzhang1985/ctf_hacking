---
layout: default
title: Stack Protection Techniques
---

<h2>{{ page.title }}</h2>


0x1 DEP / NX (No-eXecute)
---
Shellcode is not able to run on the Stack.

```
gcc -fno-stack-protector -z execstack
```

0x2 DEP / NX (No-eXecute)
---
