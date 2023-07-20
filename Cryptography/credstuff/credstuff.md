# Description
We found a leak of a blackmarket website's login credentials. <br>
Can you find the password of the user cultiris and <br>
successfully decrypt it? <br>
Download the leak here. <br>
The first user in usernames.txt corresponds to the first <br>
password in passwords.txt. The second user corresponds to <br>
the second password, and so on.

# Solution

```wget https://artifacts.picoctf.net/c/151/leak.tar```

After getting the file it is compress with tar so I ran the following command to decompress it.

```tar -xf leak.tar```

I then entered the leak directory.

```cd leak```

In this directory there are two files. usernames.txt and passwords.txt.

Based on the description I need to be looking for a user named cultiris and keeping in mind that the line in usernames.txt corresponds to the line in passwords.txt where the password is stored.

So in usernames.txt I grepped (searched) for the user cultiris with "-n" to show the line number.

```cat usernames.txt | grep -n cultiris```

It showed that it is indeed in the file at line 378.

I then used sed to get the exact line 378 in the password file. 

```sed -n '378p' passwords.txt```

The "378" dictates the line number with p dictating that is will be printed.

I orginally thought I might have to do hash cracking, but on this line was this text:

```cvpbPGS{P7e1S_54I35_71Z3}```

This looks like some form of caesar cipher so I just started with rot13 decoding and it gave the flag.

```sed -n '378p' passwords.txt | caesar 13```

I piped it into ```caeser 13``` to decode it with rot13, but you can also use cyberchef if you want. This functionality is a part of bsdgames which you can get with ```sudo apt install bsdgames```.

Flag: ```picoCTF{C7r1F_54V35_71M3}```
