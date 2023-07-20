# Description

We found this weird message being passed around on the <br>
servers, we think we have a working decryption scheme. <br>
Download the message here. <br>
Take each number mod 37 and map it to the following <br>
character set: 0-25 is the alphabet (uppercase), 26-35 are the <br>
decimal digits, and 36 is an underscore. <br>
Wrap your decrypted message in the picoCTF flag format (i.e. picoCTF{decrypted_message})

# Solution

```wget https://artifacts.picoctf.net/c/128/message.txt```

Contents of message:

165 248 94 346 299 73 198 221 313 137 205 87 336 110 186 69 223 213 216 216 177 138

The first goal is to apply mod 37 to each number. To do this I chose to do it with a python script. This means that I would want to put the numbers into an array. Since I wanted to use sed instead of some other method I used this command to turn it into the correct format for an array in python.

```cat message.txt | sed -e "s/^/[/" | sed 's/ *$//' | sed -e "s/$/]/" | sed -e "s/ /, /g"```

sed stands for stream editor and it can do many things but I'm specifically using it to transform text in this case. 

-e stands for script, you put it before the command you want to run. 

Looking at the first part, ```sed -e "s/^/[/"```, the "^" stands for at the start of the line and the the "[" stands for what will placed there.

Next, ```sed 's/ *$//'```, the "$" stands for at the end of the line, the space is what will be being removed from the end of the line, and the "*" stands for all spaces at the end of the line.

Last part, ```sed -e "s/ /, /g"```, the " " between the two / is what will being replaced with ", ".

This whole command changes the orginal contents to this:

[165, 248, 94, 346, 299, 73, 198, 221, 313, 137, 205, 87, 336, 110, 186, 69, 223, 213, 216, 216, 177, 138]

This is the python script I made to complete this challenge:

```
arr = [165, 248, 94, 346, 299, 73, 198, 221, 313, 137, 205, 87, 336, 110, 186, 69, 223, 213, 216, 216, 177, 138]
characterSet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789_"
flag = "picoCTF{"

for i in range(len(arr)):
	arr[i] = arr[i] % 37
	flag += characterSet[arr[i]]

flag += "}"
print(flag)
```

Explanation of what the python script is doing:

* Line 1: This is the input array which is what was given from the picoCTF challenge.
* Line 2: The charater set with the parameters that they gave in the description. 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore.
* Line 3: Setting a string to "picoCTF{" for wrapping the contents of the flag.
* Line 5: The for loop that iterates over the size of the array so it goes to each number.
* Line 6: Starting from (165) the first number in the array to the last (138) it applies mod 37. % is mod in python.
* Line 7: Based on the number found after the mod 37 operation it looks in the charater set to find the corresponding correct charater.
* Line 9: Adding the closing bracket to the flag string.
* Line 10: Printing the flag.

Once the script was done I ran it in the command line with this command since it's python ```python3 script.py```. This gave the flag.

Flag: ```picoCTF{R0UND_N_R0UND_B6B...}```
