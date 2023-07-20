# Description

Attackers have hidden information in a very large mass of <br>
data in the past, maybe they are still doing it. <br>
Download the data here.

# Solution

```wget https://artifacts.picoctf.net/c/126/anthem.flag.txt```

I initially did ```cat anthem.flag.txt``` and saw it was a lot of text.

Simply doing ```cat anthem.flag.txt | grep pico``` and you will see the flag. However I now am going to get just the flag and nothing else.

Since there are a lot of leading spaces I will use sed to get rid of that.

```cat anthem.flag.txt | grep pico | sed -e "s/^ *//g"```

The "-e" is to dictate the script, the "s/" and "/g" is just how sed starts and end in a script. The "^" denotes the start of the line, then the " " denotes what at the start of the line, lastly the "\*" denotes all of the spaces at the start of the line. After the "*" there is a / which after you could put something to replace all the spaces at the begining with. In this case I want it to be deleted so I put nothing there. So this is basically replacing all the spaces at the beginning of the line with nothing.

```cat anthem.flag.txt | grep pico | sed -e "s/^ *//g" | cut -d " " -f7```

Then I used cut with a space as the delimiter to look at the 7th field to get just the flag itself.

Flag: ```picoCTF{gr3p_15_@w3s0m3_2116...}```
