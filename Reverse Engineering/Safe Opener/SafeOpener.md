# Description
Can you open this safe?<br>
I forgot the key to my safe but this program is supposed to <br>
help me with retrieving the lost key. Can you help me unlock <br>
my safe? <br>
Put the password you recover into the picoCTF flag format <br>
like: <br>
picoCTF{password}

# Solution

```wget https://artifacts.picoctf.net/c/83/SafeOpener.java```

When you cat the java file out you can see in the main function it is calling an openSafe function to check if it is open. Since we are looking for the password as the flag it is likely in that function. Also take note that main function it is using base64 on the inputted string to compare to an encoded string.

![image](https://user-images.githubusercontent.com/91398631/236707629-3495bb59-75b4-4975-a35a-9a4df2a277ba.png)

Now in the openSafe function you can see the encoded password in plaintext.

![image](https://user-images.githubusercontent.com/91398631/236707700-2a7297eb-2363-4747-b230-2c1abc95455f.png)

To get the encoded key you could just copy-paste it from the output or you can run this command to only output the encoded key.

```cat SafeOpener.java | grep encodedkey | sed -n "5p" | cut -d "\"" -f2```

This line of code is first outputting the SafeOpener.java file, then it is grepping for encodedkey. Since there are multiple lines with encodedkey I am using sed -n "5p" to print the 5th line only. Lastly, I am using cut with " as the delimiter and \ to escape the charater while looking at the second field and I then get just the encoded key.

Because we know that this is base64 from the main function we can just pipe this into base64 decode.

```cat SafeOpener.java | grep encodedkey | sed -n "5p" | cut -d "\"" -f2 | base64 -d```

This will give you the password. If you wanted to check for sure you could run the file, ```java SafeOpener.java```, input the password and see "Sesame open" prooving that this is indeed the correct password.

Now we just have to wrap the outputted decoded password with picoCTF{} to get the flag. This can be done with sed.

```cat SafeOpener.java | grep encodedkey | sed -n "5p" | cut -d "\"" -f2 | base64 -d | sed -e "s/^/picoCTF{/g" | sed -e "s/$/}/g"```

^ denotes the start, and $ denotes the end. This line of code gives the flag. If you wanted you could direct this command into an getflag.sh script and run it every time you want to get the flag or just direct the output to flag.txt or of course just submit the flag by copy and pasting it.

Flag: ```picoCTF{pl3as3_l3t_m3_1nt0_th...}```
