# Description

SOS, someone is torrenting on our network. <br>
One of your colleagues has been using torrent to download <br>
some files on the company’s network. Can you identify the <br>
file(s) that were downloaded? The file name will be the flag, <br>
like picoCTF{filename}. Captured traffic.

# Solution

```wget https://artifacts.picoctf.net/c/165/torrent.pcap```

```wireshark torrent.pcap```

THe objective is to find the file(s) that were downloaded through bit torrent. This is likely going to be done with the hash. With bittorrent it's called the info_hash. I initially tried search by bittorrent.info_hash as a filter, but then realized it is with BT-DHT.

Then I used bt-dht and it gave me all of the bittorrent traffic.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/26cb479a-bdf3-43ae-a95d-65e545502c4a)

I then looked at the first packet and expanded all the subtrees for the Bit Torrent protocol. I then scrolled through the packets until I saw info_hash.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/58d9d25b-2a2a-43fc-a15a-98777de153c5)

This hash is not the correct one, so I decided to look for the info_hash that was seen the most. I did this by making info hash into a colomn.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/b6a4b160-0c7c-4827-ac62-07c683abc39b)

After that I clicked the colomn (string) to sort through it based on the info_hash and looked for the one that appeared the most.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/3875bbbb-f360-4832-9e28-a4cd8b1fc9b8)

This is the info_hash that appeared the most.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/a32c3e5e-6676-4e5a-af7a-a46b4c0eea26)

I first put it into VirusTotal and found no matches so I then put it into google.

This directed me to find that it is an .iso file through Linuxtracker (first google result).

Flag: ```picoCTF{.....amd64.iso}```
