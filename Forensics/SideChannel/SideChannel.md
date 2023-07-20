# Description

There's something fishy about this PIN-code checker, can you <br>
figure out the PIN and get the flag? <br>
Download the PIN checker program here pin_checker <br>
Once you've figured out the PIN (and gotten the checker <br>
program to accept it), connect to the master server using nc <br>
saturn.picoctf.net 53639 and provide it the PIN to get your flag.

Hint 1: Read about "timing-based side-channel attacks."

# Solution

```wget https://artifacts.picoctf.net/c/74/pin_checker```

Then ```sudo chmod +x pin_checker``` to be able to run the file.

The key realisation here is to notice that the amount of time it takes to return (when given a valid 8 number pin) changes for every correct number. The more correct numbers the longer it takes to return.

You can test it out with this command:

Orginal: ```echo "11111111" | time ./pin_checker```

Changed: ```echo "41111111" | time ./pin_checker```

You can see that the time changes between a valid 8 digit pin that has most digits wrong, to one with at least one digit correct. Once I had this realisation I was able to create the python script below to automate this process and find the pin.

```
from pwn import *
import time

context.log_level = "critical"

elf = ELF("./pin_checker")

pin = "11111111"
finalPin = "11111111"

currentElapsed = 0

for i in range(0, 8):
    for j in range(0, 10): 
        p = elf.process()

        arr = list(pin)
        arr[i] = str(j)
        pin = "".join(arr)

        p.sendline(pin.encode())
        before = time.perf_counter()
        response = p.recvall().decode("latin-1")
        after = time.perf_counter()

        elapsed = after - before

        if elapsed > currentElapsed:
            arr = list(pin)
            arr[i] = str(j)
            finalPin = "".join(arr)
            currentElapsed = elapsed
    pin = finalPin

print(pin)
```

Explaing the python script:
* Line 1/2: Importing all of pwntools which is used to run the elf file as well as importing time so I could create a counter later on in the code.
* Line 4: Setting the context.log_level to critical to get rid of the pwntools output every time it makes and closes a connection.
* Line 6: Setting ./pin_checker into the elf variable that will be used latter to start a process.
* Line 8/9: Setting pin/finalPin variable to be used later. Inialized to 8 digit pin consisting of just 1's.
* Line 11: Setting currentElapsed variable to 0.
* Line 13: This is the first for loop. It will iterate 0-7 (8 times) for each digit in the pin.
* Line 14: This is the second for loop which is nested in the first. It will iterate 0-9 (10 times) for each number possible to try.
* Line 15: Starts a new process every single loop.
* Line 17-19: Creating an array of the pin. "i" stands for the current position in the pin, so arr[i] will only change that position. Then for that position in each loop that iterates 10 times for each digit it will change the digit each time. This is to test all values and elapsed times. Lastly, it is put back into pin with the changes.
* Line 21: Sending the current pin.
* Line 22: Starting the timer right after the data was sent.
* Line 23: Received all of the data.
* Line 24: Ending the timer rigth after the data was received.
* Line 26: Calculating the elapsed time and putting it into the elapsed variable.
* Line 28: Checking if the elasped time for that iteration is bigger than currentElasped. For the first iteration it will always be bigger as currentElasped was set to 0. But then after currentElapsed is set to elapsed later on in the if statement than in the next iteration it will have to be bigger than that. Since the time grows with each correct number cumaltivly currentElasped is never reset.
* Line 29/31: These lines do the same thing that lines 17-19 did. Only difference is that the correct number is saved into finalPin. It could have been set to pin and then break when found it, but this is the way I orginally did it.
* Line 32: Now setting currentElasped equal to elasped when in this if statment.
* Line 33: Outside the second for loop and in the first for loop pin is now set to finalPin.
* Line 35: Outside both for loops when everything is done the correct pin is printed to output.

After completing the script I ran ```python3 script.py``` and it gave me the right pin. 

Then I connected with this command: ```nc saturn.picoctf.net 53639```.

After inputting the correct pin the flag was given.

Flag: ```picoCTF{t1m1ng_4tt4ck_914c...}```

