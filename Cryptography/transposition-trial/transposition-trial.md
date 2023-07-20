# Description

Our data got corrupted on the way here. Luckily, nothing got <br>
replaced, but every block of 3 got scrambled around! The first <br>
word seems to be three letters long, maybe you can use that <br>
to recover the rest of the message. <br> 
Download the corrupted message here.

# Solution

```wget https://artifacts.picoctf.net/c/191/message.txt```

First it is needed to understand what is happening and how the file is encoded.

Here is the encoded text: ```heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V6E5926A}4```

Based on the description it is known that there is mutliple blocks of three that are scrambled. It is also given that the first word is three letters long. 

From looking at the text the first word looks like "the", then maybe "flag", and can idetify the flag picoCTF{} in the line as well.

In the title, "transposition" , is a hint that the letters need to move positions. From looking at the first word it becomes obvious how to make that correct.

From "heT" to "The". So the third position moves to the first position, the first position moves to the second posiiton, and the second position moves to the third position. Once these operations are done it is then in the correct order.

Then I wrote a python script to do this for every block of three in the entire line of text.

Here is the python script used to get the flag.

```
flag = ""

with open("message.txt") as file:
	message = file.read()

	for i in range(0, len(message), 3):
		flag += message[i+2:i+3] + message[i:i+1] + message[i+1:i+2]

	print(flag.split()[-1])
```

Explaination of python script:
* Line 1: Initializing the flag variable as a string.
* Line 3: Opening message.txt as file. This is the encoded file downdloaded from the challenge.
* Line 4: Putting the contents of the file into the message variable by reading file.
* Line 6: A loop that goes for the length of message but counts in increments of three.
* Line 7: Adds to the flag variable the correctly shifted version.
* Line 9: Printing out the last part of the decoded sentance which is only the flag itself.

Flag: ```picoCTF{7R4N5P051N6_15_3XP3N51V3_56E6...}```
