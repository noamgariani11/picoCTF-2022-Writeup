# Description

A type of transposition cipher is the rail fence cipher, which is <br>
described here. Here is one such cipher encrypted using the <br>
rail fence with 4 rails. Can you decrypt it? <br>
Download the message here. <br>
Put the decoded message in the picoCTF flag format, <br>
picoCTF{decoded_message}.

# Solution

The provided a wiki page to where it shows how to decode this message manually, but I justed used cyberchef.

Encoded Message: ```Ta _7N6D49hlg:W3D_H3C31N__A97ef sHR053F38N43D7B i33___N6```

Because it said in the description that it is the rail fence cipher with 4 rails I used rail fence decode with the key being set to 4.

![image](https://user-images.githubusercontent.com/91398631/236644100-cf656e26-68ee-47c8-90f7-f06e56a5ccd5.png)

This gaved the decoded message:

![image](https://user-images.githubusercontent.com/91398631/236644126-5d46c9c6-43ec-496f-9362-6b657a42ec15.png)

Flag: ```picoCTF{WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_4A76...}```
