# Description

Can you get the flag?

Run this Python program in the same directory as this encrypted flag.

# Solution

```wget https://artifacts.picoctf.net/c/103/bloat.flag.py```

```wget https://artifacts.picoctf.net/c/103/flag.txt.enc```

First thing I did was ```cat bloat.flag.py``` to see what is in the file.

![image](https://user-images.githubusercontent.com/91398631/236709212-c5eaa016-c56f-4082-8d3b-a74e550f4be9.png)

It looks like there was a variable "a" that was made and the code is obfuscated with this. To deobfuscate this I opened the file in a text editor and used the python command line in linux to look line by line what teh code is trying to do.

To get into python you just run ```python```.

Then I put in to initialize "a" variable:

```
a = "!\"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ"+ \
            "[\\]^_`abcdefghijklmnopqrstuvwxyz{|}~ "
```

Now I can just do print() and any of the lines with a[] and get clear text. Now I started replacing in the text editor what I found with python.

![image](https://user-images.githubusercontent.com/91398631/236709387-8a07fe2d-7d41-4a9e-a4d2-3158418ed75a.png)

You can do this for all of it if you wanted. Using control z to exit python.

Now this is what the code looks after I deobfuscated it.

![image](https://user-images.githubusercontent.com/91398631/236709530-789f7cab-56a4-4148-9852-9de5435946e3.png)

Near the top of the file you can see the password "happychance" in plain text. You can now run the file ```python3 bloat.flag.py```, pyt in the correct password, and get the flag.

If you wanted to get just the flag you can run this command.

```python3 bloat.flag.py | tee output.txt```

Then using sed to get the second line in output which would be just the flag.

```cat output.txt | sed -n "2p"```

That gives just the flag.

Flag: ```picoCTF{d30bfu5c4710n_f7w_b80...}```
