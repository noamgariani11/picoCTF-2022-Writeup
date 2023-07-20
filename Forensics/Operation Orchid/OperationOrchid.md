# Description

Download this disk image and find the flag. <br>
Note: if you are using the webshell, download and extract the <br>
disk image into /tmp not your home directory. 
* Download compressed disk image

# Solution

```wget https://artifacts.picoctf.net/c/214/disk.flag.img.gz```

After going through some of the directories after loading the disk image in autopsy I decided to do a keyword search for "flag.txt".

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/a0b28761-af2b-4538-b56d-20bcc5011dbc)

This showed me bash history and that a flag.txt.enc and flag.txt file exist.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/f5889400-0ea6-4e46-8335-e1ab521f15e8)

In the bash history you can see how the encoded flag.txt to flag.txt.enc.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/2b493d9d-03a2-4bef-932d-d4beb933eb60)

Now going to file search for "flag.txt" you can see that flag.txt was deleted but "flag.txt.enc" is still there.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/c4631cd5-42ec-46b5-a2ca-1b466b91b3f4)

From this point I used export in autopsy to get the file on my system. I then moved it from downloads to my working directory with "mv". I then renamed it to "flag.txt.enc"

```mv vol4-3.root.flag.txt.enc flag.txt.enc```

Looking at there command only some slight changes need to be made to decrypt the file:

Orginal (to encode): ```openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567```

Modified (to decode): ```openssl aes256 -salt -in flag.txt.enc -out flag.txt -k unbreakablepassword1234567 -d```

After running the decoding openssl command a flag.txt file is created. All that is needed now is to do ```cat flag.txt``` and you get the flag.

Flag: ```picoCTF{h4un71ng_p457_1d02...}```
