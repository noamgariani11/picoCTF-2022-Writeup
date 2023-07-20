# Description

Can you get the flag?

Download this binary.

Here's the test drive instructions:
* $ chmod +x gdbme
* $ gdb gdbme
* (gdb) layout asm
* (gdb) break *(main+99)
* (gdb) run
* (gdb) jump *(main+104)

# Solution

```wget https://artifacts.picoctf.net/c/85/gdbme```

After getting the file it is really just running the commands that they said in the instructions.

* ```sudo chmod +x gdbme```
* ```gdb gdbme```
* ```(gdb) layout asm```
* ```(gdb) break *(main+99)```

![image](https://user-images.githubusercontent.com/91398631/236706883-2aa77ccf-f106-4d5d-8004-3ffb51c2b09c.png)

* ```(gdb) run```
* ```(gdb) jump *(main+104)```

![image](https://user-images.githubusercontent.com/91398631/236706966-3cfb723d-e045-4435-a87f-ea4b9d24867d.png)

Then the flag is presented after you jump to main+104 skipping the sleep.

Flag: ```picoCTF{d3bugg3r_dr1v3_197c3...}```

