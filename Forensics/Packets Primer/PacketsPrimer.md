# Description

Download the packet capture file and use packet analysis <br>
software to find the flag.
* Download packet capture

# Solution

```wget https://artifacts.picoctf.net/c/196/network-dump.flag.pcap```

I first just tried to run strings before even running it in wireshark and I saw the flag.

```strings network-dump.flag.pcap```

![image](https://user-images.githubusercontent.com/91398631/236730401-3c3e6bee-a3e7-4563-80dc-e57cfef2aeb2.png)

The flag is on the 8th line so I used sed to get just the 8th line.

```strings network-dump.flag.pcap | sed -n "8p"```

Then I used tr to get rid of all the spaces.

```strings network-dump.flag.pcap | sed -n "8p" | tr -d " "```

This line gives just the flag with not spaces.

Flag: ```picoCTF{p4ck37_5h4rk_01b0...}```
