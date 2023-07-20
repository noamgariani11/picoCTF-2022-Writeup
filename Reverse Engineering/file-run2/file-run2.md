# Description

Another program, but this time, it seems to want some input. <br>
What happens if you try to run it on the command line with <br>
input "Hello!"? <br>
Download the program here.

# Solution

```wget https://artifacts.picoctf.net/c/155/run```

This is very similiar to file-run1, but the only differance is you are passing in an argument to the executable.

After running ```sudo chmod +x run``` to change the permissions you can try running ```./run``` but it will tell you that it wants an argument.

If you do anything other than "Hello!" as specified in the description like ```./run hello``` it will ask you to say "Hello!".

Once you put in the correct argument, ```./run Hello!```, then you will get the flag.

If you wanted just the flag and nothing else you can use cut with a space as the delimeter and looking at the fourth field.

```./run Hello! | cut -d " " -f4```

Flag: ```picoCTF{F1r57_4rgum3n7_be07...}```
