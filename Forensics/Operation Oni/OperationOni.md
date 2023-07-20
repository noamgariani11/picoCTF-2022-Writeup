# Description

Download this disk image, find the key and log into the <br>
remote machine. <br>
Note: if you are using the webshell, download and extract <br>
the disk image into /tmp not your home directory.
- Download disk image
- Remote machine: ```ssh -i key_file -p 53918 ctf-player@saturn.picoctf.net```

# Solution

```wget https://artifacts.picoctf.net/c/69/disk.img.gz```

After getting the disk image and running, ```gunzip disk.img.gz```, I loaded the file into autopsy with ```sudo autopsy```. A similar process was shown in my SleuthkitApprentice writeup.

Based on the previous challenge the flag was in the root directory, so I checked the root directory and in the folder .ssh folder was the ssh key mentioned in the description that is needed to get into the machine.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/f6882b2f-f95e-4f88-a283-fe377632d836)

I then clicked export to get the ssh key. Then I used "mv" to move the file from downloads to my working directory.

To match the syntax in the given command in the description I changed the file name to "key_file".

```mv vol3-2.root..ssh.id_ed25519 key_file```

I then tried running the command to get into the machine.

```ssh -i key_file -p 53918 ctf-player@saturn.picoctf.net```

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/5d62627c-0ac9-43a6-b374-513fb4efab28)

However this gave me permission issues and then I remembered that for the ssh key it need to also be set to 600 permission.

1 is execute, 2 write, and 4 is read. So 6 would be only read and write with no execute. Only 1 would be just execute and so on. The first number is the three numbers is standing for the users/owners permissions, the second one is for the group, and the third is for others. 

```chmod 600 key_file```

After running this command I tried logging in again and it worked.

```ssh -i key_file -p 53918 ctf-player@saturn.picoctf.net```

I then did ```ls``` and found there was just a flag.txt file. If you do ```cat flag.txt``` you will see the flag.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/f1c56ff3-4eec-44ed-949b-83e55eb5cb83)

Flag: ```picoCTF{k3y_5l3u7h_3396...}```
