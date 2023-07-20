# Description

Download this packet capture and find the flag.
- Download packet capture

# Solution

```wget https://artifacts.picoctf.net/c/135/capture.flag.pcap```

For this challenge I used tcpflow on the pcap file. You can do it through wireshark as well though.

Run this command to install tcpflow if you don't already have it.

```sudo apt install tcpflow -y```

Then I ran this command:

```tcpflow -r capture.flag.pcap```

This gets all the transmitted file with "tcpflow -r". Here are all the files in the working directory so far after running tcpflow.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/5b5b7ef2-6867-4041-a00d-987fad888be2)

The sending/received ip's are at the start and then the port that it is over for the way the files are named.

Afer running ```file *``` it is clear what files contain what.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/c72f20da-a523-4eee-bd49-3251710ed17d)

I started with this command (because that file was the first ascii text file): ```cat 010.000.002.004.09001-010.000.002.015.57876```. This gave one side of a converstation.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/7eb37cc0-5c49-4ce4-afb4-c988a488f6e1)

I then went on to the next ascii text file in hopes this was the other side of the converstation (which it was): ```cat 010.000.002.015.57876-010.000.002.004.09001```. This side of the converstation looked like this:

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/f2c51942-2619-4aa1-9413-c53361682a80)

First big thing is it shows how to decrypt the file: ```openssl des3 -d -salt -in file.des3 -out file.txt -k supersecretpassword123```.

Second thing it says that the file is over port 9002. 

There was only one file that was extracted over port 9002.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/ddefd273-a5e8-43c2-ba84-e2e5fe279455)

And this file shows that it is "openssl enc'd data with salted password" which matches what is expected.

I then did this command: ```mv 010.000.002.015.56370-010.000.002.004.09002 file.des3```. This was done to match the syntax of there given command.

Then I ran the openssl decrypting line: ```openssl des3 -d -salt -in file.des3 -out file.txt -k supersecretpassword123```.

Since the output file is called file.txt I then did ```cat file.txt``` and the flag was displayed from that file.

Flag: ```picoCTF{nc_73115_411_0ee72...}```
