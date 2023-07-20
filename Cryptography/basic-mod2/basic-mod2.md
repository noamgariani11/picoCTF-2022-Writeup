# Description

A new modular challenge! <br>
Download the message here. <br>
Take each number mod 41 and find the modular inverse for  <br>
the result. Then map to the following character set: 1-26 are <br>
the alphabet, 27-36 are the decimal digits, and 37 is an underscore. <br>
Wrap your decrypted message in the picoCTF flag format (i.e. picoCTF{decrypted_message})

# Solution

```wget https://artifacts.picoctf.net/c/180/message.txt```

This python script is heavily built on the one explained in [basic-mod1](https://github.com/noamgariani11/picoCTF-2022-Writeup/blob/main/Cryptography/basic-mod1/basic-mod1.md).

This command: ```cat message.txt | sed -e "s/^/[/" | sed 's/ *$//' | sed -e "s/$/]/" | sed -e "s/ /, /g"``` results in the correct format for the array in python.

```
arr = [268, 413, 438, 313, 426, 337, 272, 188, 392, 338, 77, 332, 139, 113, 92, 239, 247, 120, 419, 72, 295, 190, 131]
characterSet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789_"
flag = "picoCTF{"

for i in range(len(arr)):
        arr[i] = pow(arr[i], -1, 41)
        flag += characterSet[arr[i]-1]

flag += "}"
print(flag)
```

The only change in the script beyond the different input array is the mod operation line.

```pow(arr[i], -1, 41)``` does the modular inverse for the result assuming mod 41.

To run the python script: ```python3 script.py```. Assuming you named the python script, script.py.

Flag: ```picoCTF{1NV3R53LY_H4RD_8A05...}```
