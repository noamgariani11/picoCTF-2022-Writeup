# Description

A message has come in but it seems to be all scrambled. <br>
Luckily it seems to have the key at the beginning. Can you <br>
crack this substitution cipher? <br>
Download the message here.

# Solution

Since it's known that it is a subsition cipher and they say the key is at the beginning it should be easy to do with a python script.

```
characterSet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
key = "ZGSOCXPQUYHMILERVTBWNAFJDK"
enc_flag = "5NG5717N710L_3A0MN710L_357GX9XX"
flag = "picoCTF{"

for i in range(len(enc_flag)):
        if enc_flag[i].isupper():
                flag += characterSet[key.index(enc_flag[i])]
        else:
                flag += enc_flag[i]

flag += "}"
print(flag)
```

Explanation of the python script:

* Line 1: The charater set. As in just the alphabet all upercase.
* Line 2: The key found at the beginning of the file.
* Line 3: The inside of what looked to be the flag at the end of the file initialized to an enc_flag variable. I didn't include the whole flag so I can go on the assumption that I am only dealing with uppercase letters.
* Line 4: Initializing the decoded flag with "picoCTF{" as a start.
* Line 6: A for loop that will iterate over every letter inside enc_flag
* Line 7: If the charater in enc_flag that it is currently looking at is an uppercase letter than it will do the subsitution.  
* Line 8: It adds the subsituted version to the flag variable. To start key.index(enc_flag[i]) gets the char in enc_flag and finds the position/index that it has in the key. Then charaterSet[] around that value takes the uppercase alphabet and uses the corresponding index. Once the correct letter is found it's added to the flag variable
* Line 9/10: Otherwise if it's anything else (not uppercase) like a number or underscore it will just add the charater normally to the flag variable.
* Line 12: Adding the closing bracket to the flag variable.
* Line 13: Printing out the flag.

After running the python script, ```python3 script.py```, the flag is sucessfully retrevied.

Flag: ```picoCTF{5UB5717U710N_3V0LU710N_357...}```

