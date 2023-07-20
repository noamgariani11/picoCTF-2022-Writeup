# Description

A program has been provided to you, what happens if you try <br>
to run it on the command line? <br>
Download the program here.

# Solution

```wget https://artifacts.picoctf.net/c/219/run```

After getting the file, you can run file to see what type of file it is.

```file run```

You'll see that it is a "ELF 64-bit LSB pie executable", so change the permissions to add the ability to execute the file.

```sudo chmod +x run```

The with "./" then the file name you can run the file.

```./run```

After running the file you will see the flag.

```./run | cut -d " " -f4```

If you wanted to get just the flag and nothing else you can use cut with a space as the delimeter and looking at the fourth field. This will get you just the flag.

Flag: ```picoCTF{U51N6_Y0Ur_F1r57_F113_e55...}```
