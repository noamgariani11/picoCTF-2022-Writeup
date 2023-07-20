# Description

Download this image and find the flag.
* Download image

# Solution

```wget https://artifacts.picoctf.net/c/217/pico.flag.png```

It is as simple as just running zsteg. 

```zteg pico.flag.png```

This gives the flag, but you can also do this to get the flag into flag.txt.

```zteg pico.flag.png > output.txt```

And then to only get the flag.

```cat output.txt | grep pico | cut -d "\"" -f2 | cut -d "$" -f1 > flag.txt```

Then do ```cat flag.txt``` to get the flag.

Flag: ```picoCTF{7h3r3_15_n0_5p00n_a9a1...}```
