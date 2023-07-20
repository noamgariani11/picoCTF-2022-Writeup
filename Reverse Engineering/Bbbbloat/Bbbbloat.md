# Description

Can you get the flag?

Reverse engineer this binary.

# Solution

I first tried to create a python script to brute force it.

```
#!/usr/bin/env python

from pwn import *

context.log_level = "critical"

elf = ELF("./bbbbloat")

for i in range(100000):
    p = elf.process()
    p.sendline(str(count+i).encode())
    response = p.recvall(timeout=0.01).decode("latin-1")
    if "Sorry" not in response:
        print(response)
```

This was not the intended solution and it took forever to complete. It would probably eventually give the right answer, but I then moved on to Ghidra.

This is how I found it with Ghidra:

...

Also after finding it in Ghidra I went back to the script and put it at 50000 and it found the right number in a minute or so.

Flag: ```picoCTF{cu7_7h3_bl047_69...}```
