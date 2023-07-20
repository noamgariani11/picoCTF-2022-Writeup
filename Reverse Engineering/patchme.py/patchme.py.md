# Description

Can you get the flag?

Run this Python program in the same directory as this encrypted flag.

# Solution

```wget https://artifacts.picoctf.net/c/201/patchme.flag.py```

```wget https://artifacts.picoctf.net/c/201/flag.txt.enc```

I then looked at both files and found this in the python file.

![image](https://user-images.githubusercontent.com/91398631/236707210-04efb9ed-ccb8-4a2e-a107-f94087d1116c.png)

This basically gives the password in plaintext in the function.

I then ran the python script: ```python3 patchme.flag.py```

And entered the password given in the function ```ak98-=90adfjhgj321sleuth9000``` and the flag was given.

Also if you wanted to just get the flag you can first run this command to direct the output to a file.

```python3 patchme.flag.py | tee output.txt```

Then all you have to do is grep for "pico".

```cat output.txt | grep pico```

If you want to put that in a flag.txt file you could do this.

```cat output.txt | grep pico > flag.txt```

Then ```cat flag.txt``` should give you just the flag.

Flag: ```picoCTF{p47ch1ng_l1f3_h4ck_f01e...}```
