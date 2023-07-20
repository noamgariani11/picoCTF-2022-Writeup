# Description

It seems that another encrypted message has been <br>
intercepted. The encryptor seems to have learned their lesson <br>
though and now there isn't any punctuation! Can you still <br>
crack the cipher? <br>
Download the message here.

# Solution

```wget https://artifacts.picoctf.net/c/113/message.txt```

This is very similar to substitution1, but it has no punction or spaces.

Cipher Text:

isnfnnpctitnznfmxhisnfwnxxntimjxctsnascdstushhxuhgqbinftnubfciruhgqnicichktckuxbackdurjnfqmifchimkabturjnfusmxxnkdnisntnuhgqnicichktehubtqfcgmfcxrhktrtingtmagckctifmichkebkamgnkimxtwscusmfnznfrbtnebxmkagmfonimjxntocxxtshwnznfwnjnxcnznisnqfhqnfqbfqhtnhemscdstushhxuhgqbinftnubfciruhgqnicichkctkhihkxrihinmuszmxbmjxntocxxtjbimxthihdnitibankitckinfntinackmkanpucinamjhbiuhgqbinftucnkunanenktcznuhgqnicichktmfnheinkxmjhfchbtmeemcftmkauhgnahwkihfbkkckdusnuoxctitmkanpnubickduhkecdtufcqitheenktnhkisnhisnfsmkactsnmzcxrehubtnahknpqxhfmichkmkacgqfhzctmichkmkaheinksmtnxngnkitheqxmrwnjnxcnznmuhgqnicichkihbusckdhkisnheenktcznnxngnkitheuhgqbinftnubfcirctisnfnehfnmjniinfznscuxnehfinusnzmkdnxctgihtibankitckmgnfcumkscdstushhxtebfisnfwnjnxcnznismimkbkanftimkackdheheenktczninuskcvbntctnttnkicmxehfghbkickdmkneenuicznanenktnmkaismiisnihhxtmkauhkecdbfmichkehubtnkuhbkinfnackanenktcznuhgqnicichktahntkhixnmatibankitihokhwisncfnkngrmtneenuicznxrmtinmusckdisngihmuicznxrisckoxconmkmiimuonfqcuhuiectmkheenktcznxrhfcnkinascdstushhxuhgqbinftnubfciruhgqnicichkismitnnotihdnknfminckinfntickuhgqbinftucnkunmghkdscdstushhxnftinmusckdisngnkhbdsmjhbiuhgqbinftnubfcirihqcvbnisncfubfchtcirghiczmickdisngihnpqxhfnhkisncfhwkmkankmjxckdisngihjniinfanenkaisncfgmusckntisnexmdctqcuhUIE{K6F4G_4K41R515_15_73A10B5_702E03EU}

I tried putting it into [quipqiup](https://quipqiup.com/) again and it partially worked.

Decoded Text:

there exist several other well established high school computer security competitions including cyber patriot and us cyber challenge these competitions focus primarily on systems administration fundamentals which are very useful and marketable skills however we believe the proper purpose of a high school computer security competition is not only to teach valuable skills but also to get students interested in and excited about computer science defensive competitions are often laborious affairs and come down to running checklists and executing config scripts offense on the other hand is heavily focused on exploration and improvisation and often has elements of play we believe a competition touching on the offensive elements of computer security is therefore a better vehicle for tech evangelism to students in american high schools further we believe that an understanding of offensive techniques is essential for mounting an effective defense and that the tools and configuration focus encountered in defensive competitions does not lead students to know their enemy as effectively as teaching them to actively think like an attacker pico c t f is an offensively oriented high school computer security competition that seeks to generate interest in computer science among high schoolers teaching them enough about computer security to pique their curiosity motivating them to explore on their own and enabling them to better defend their machines the flag is pico c t f n r m ny duff c

So it mostly got it right but the flag portion which I assume is because the underscores and numbers.

Here is a side by side comparison:

pico c t f n r m ny duff c

qcuhUIE{K6F4G_4K41R515_15_73A10B5_702E03EU}

If you just manually substitute the letters after pico c t f into the encoded version, but only the letters than you get the correct flag.

Flag: ```picoCTF{N6R4M_4N41Y515_15_73D10U5_702F03FC}```
