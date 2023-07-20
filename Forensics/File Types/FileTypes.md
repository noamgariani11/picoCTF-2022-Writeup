# Description

This file was found among some files marked confidential but <br>
my pdf reader cannot read it, maybe yours can. <br>
You can download the file from here.

# Solution

```wget https://artifacts.picoctf.net/c/80/Flag.pdf```

After doing ```cat Flag.pdf``` you can see that this looks like a script and at the top of the file it says to run the file with sh.

![image](https://user-images.githubusercontent.com/91398631/236724973-55d91c53-b7bc-46a8-aef7-6b9549b8637a.png)

When doing ```sh Flag.pdf``` I got this message:

![image](https://user-images.githubusercontent.com/91398631/236725091-0f94330d-d84a-43e2-9488-e1430b6782ca.png)

This can be fixed by getting shell archive utilities with ```sudo apt install sharutils```.

![image](https://user-images.githubusercontent.com/91398631/236725223-55ddfb73-93bb-4906-b21c-27fe4aed24d7.png)

Now it created a new file called "flag".

![image](https://user-images.githubusercontent.com/91398631/236725265-4445f253-c8e3-47d1-ad02-b29c9770b17b.png)

By look in ```man ar``` you can see that "x" is how you extract.

![image](https://user-images.githubusercontent.com/91398631/236725506-9aeb4369-b935-4087-9b3e-4dc1bf7a9772.png)

```ar x flag```

That now gives another file.

![image](https://user-images.githubusercontent.com/91398631/236725554-ba2ba9d6-b138-4f66-9daf-f4011adc2cfd.png)

After running file once again it shows that it is a cpio archive. Once again looking at the man page to see the correct syntax for extracting.

```cpio --file flag -i```

This didn't work because of a file collision because there is no file exentsion. To fix this just do ```mv flag flag.cpio```, then run ```cpio --file flag.cpio -i``` again.

Running file on the output of that shows "bzip2 compressed data". Looking at the man page again for syntax and than running this command ```bzip2 flag -d```.

That create flag.out which is gzip compressed data. I then did ```gunzip flag.out```, but it didn't know the suffix. So I did ```mv flag.out flag.gz``` then ```gunzip flag.gz```.

This gave another file called flag which is lzip compressed data. I then had to do ```sudo apt install lzip```. From there I once again looked at the man page for syntax. It can be assumed you can find the correct syntax for decompression in the man page every time. I then did ```lzip flag -d```.

This gave a flag.out file which was LZ4 compressed data.

I had to do ```sudo apt install lz4```. Then I did ```lz4 flag.out -d``` which gave an error because of the extension so I did ```mv flag.out flag.lz4```. lz4 -d is the same as unlz4 so I now did ```unlz4 flag.lz4``` and it gave another file called flag.

This file is LZMA compressed data. I then did ```lzma flag -d```, error because of suffix. ```mv flag flag.lzma``` then ```lzma flag.lzma -d```. This gave another file called flag.

This file is lzop compressed data. I then had to do ```sudo apt install lzop```. Then ```lzop flag -d```, then because of unknown suffix error ```mv flag flag.lzop```. Now I could do ```lzop flag.lzop -d```.

This gave another file named flag which is once again using lzip compressed data. So I did ```lzip flag -d```.

This then gave a flag.out file which is XZ compressed data. I then did ```unxz flag.out```, unknown suffix error so ```mv flag.out flag.xz```. Then ```unxz flag.xz```.

This gave another flag file which when running "file" finally showed ascii text.

![image](https://user-images.githubusercontent.com/91398631/236728003-942e7969-6042-4308-93c0-da2605a5aa38.png)

However when I cat the file out, ```cat flag```. It gives something that looks encoded in hexadecimal.

![image](https://user-images.githubusercontent.com/91398631/236728103-dc18feb0-31ed-42dc-a15a-e3c83c05c49b.png)

Then by runing this, ```cat flag | xxd -r -p```, it decodes the output and gives the flag. "-r" is to reverse the hex, and "-p" is to print it out.

Flag: ```picoCTF{f1len@m3_m@n1pul@t10n_f0r_0b2cur17y_3c7...}```
