# Description

Download the disk image and use ${\color{orange}mmls}$ on it to find the size of <br>
the Linux partition. Connect to the remote checker service to <br>
check your answer and get the flag. <br>
Note: if you are using the webshell, download and extract the <br>
disk image into /tmp not your home directory.
* Download disk image
* Access checker program: ${\color{orange}nc}$  ${\color{orange}saturn.picoctf.net}$  ${\color{orange}52472}$

# Solution

```wget https://artifacts.picoctf.net/c/164/disk.img.gz```

You first run the mmls command. 

```mmls disk.img```

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/644ca439-ed16-4034-9608-7d932a6c8cb4)

This gives you all the neccessary information to get the flag. Now just connected with netcat.

```nc saturn.picoctf.net 52472```

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/b70df274-c2f7-4c8b-82d4-a11b44480e35)

Then it gives the flag.

Flag: ```picoCTF{mm15_f...}```
