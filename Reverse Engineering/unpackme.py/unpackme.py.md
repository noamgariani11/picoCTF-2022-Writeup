# Description

Can you get the flag?

Reverse engineer this Python program.

# Solution

```wget https://artifacts.picoctf.net/c/48/unpackme.flag.py```

Then I just cat out the file to understand what it was doing.

![image](https://user-images.githubusercontent.com/91398631/236708477-58fd9035-b402-407f-beae-33d24bfe449d.png)

It seems to be decoding a string and once decoded it runs that code with exec().

So I then went into a text editor. You could use nano, vim, whatever you want. I used sublime (subl). And printed out plain.decode() which is what was going to be the code that was executed.

This is what it looked like with my modification:

![image](https://user-images.githubusercontent.com/91398631/236708621-b60ac3f3-9fea-4691-9447-c4a0b97bc89f.png)

I now ran the file: ```python3 unpackme.flag.py```

![image](https://user-images.githubusercontent.com/91398631/236708638-77cf2d3d-77bd-4969-9ede-9b041b4eb319.png)

With this output it gives the flag and the password in plaintext (batteryhorse).

Now that I know it's not malicious code being executed and I now the password I can revert the file back to it's orginal form and run it. After running it and putting in the correct password it gives the flag.

```python3 unpackme.flag.py | tee output.txt```

Then you can run this command to just get the flag from the output file.

```cat output.txt | cut -d " " -f4```

If you wanted you could redirect this to a flag.txt, but that output will just be the flag.

Flag: ```picoCTF{175_chr157m45_5274...}```
