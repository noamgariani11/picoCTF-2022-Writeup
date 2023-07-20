# Description

Morse code is well known. Can you decrypt this? <br>
Download the file here. <br>
Wrap your answer with picoCTF{}, put underscores in place of <br>
pauses, and use all lowercase.

# Solution

```wget https://artifacts.picoctf.net/c/79/morse_chal.wav```

I used this site to decode the morse code:

https://morsecode.world/international/decoder/audio-decoder-adaptive.html

Although since it's only 28 seconds if you wanted you code easily do it your self.

The output from the website was "WH47 H47H 90D W20U9H7", to where I then ran the following command to put it in the correct format described in the description.

```echo "WH47 H47H 90D W20U9H7" | tr -s " " "_" | sed 's/^/picoCTF{/g' | sed 's/$/}/g'```

The first part uses tr to subsitute all spaces for underscores. Then "^" in sed dictates start of line and I added picoCTF{ with that part. Then "$" dictating the end of line with sed I added "}" to the line.

Flag: ```picoCTF{WH47_H47H_90D_W20...}```
