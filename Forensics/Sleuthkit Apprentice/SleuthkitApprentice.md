# Description

Download this disk image and find the flag. <br>
Note: if you are using the webshell, download and extract the <br> 
disk image into /tmp not your home directory. 
- Download compressed disk image

# Solution

Start with getting the file:

```wget https://artifacts.picoctf.net/c/136/disk.flag.img.gz```

Then unzipping it (since it's a large file it might take some time):

```gunzip disk.flag.img.gz```

Then opening it in autopsy. Also a note that this process is asumming you are using the linux version of autopsy and not other versions (windows).

# Getting the disk into Autopsy

```sudo autopsy```

Open the link provided: ```http://localhost:9999/autopsy```

Click "New Case". 

![image](https://user-images.githubusercontent.com/91398631/232164990-5de3e85c-53b3-47c8-ac89-bcfec4e0a7d4.png)

Then fill in the "Case Name" and "Investigator Name" and click "New Case" again. 

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/e3156497-3b81-4049-88fb-1952aa1843b5)

Then click "add host" with the default investigator name.

![image](https://user-images.githubusercontent.com/91398631/232165281-256283ef-d832-4e9c-a0a3-54a4adcf3864.png)

No need to change any of the defualts, just click "add host" again. 

![image](https://user-images.githubusercontent.com/91398631/232165302-5a62c429-ce62-4b16-9553-abdfd26ba5be.png)

Then click "add image" 

![image](https://user-images.githubusercontent.com/91398631/232165368-847dbd91-222a-491f-8848-a6b597b856e2.png)

Then "add image file". 

![image](https://user-images.githubusercontent.com/91398631/232165409-f8e6a997-bc83-4b81-ab7b-426cd51df8d2.png)

To find the Location (full path) of the file run this command: ```realpath disk.flag.img```

![image](https://user-images.githubusercontent.com/91398631/232165425-82ccd2fb-338d-4e29-adc3-02ac3ccd766a.png)

It will give you the full path of that file. Alterantivly you can use pwd and then just append the file name to the end manually. Once you put the full path of the file in press "next".

Now just click "add", again with just the defualts.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/c9caebcf-09c6-4632-8679-a44e0368d35b)

Then "Ok".

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/6f488b8a-1e57-45a8-8168-522cacd1c922)

I then selected "3" as it was the largest image, then clicked analyze.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/1f1992e9-0e0a-4713-beeb-e86c5b1a922f)

Then click "File Analysis".

![image](https://user-images.githubusercontent.com/91398631/232165633-69156a75-1714-4991-b75c-aae86599ddd1.png)

I then clicked "Expand Directories" for convenience when going through the disk image.

![image](https://user-images.githubusercontent.com/91398631/232165674-2df952c3-d0ca-40e9-9e4c-edf90f648190.png)

# Findings

I first went to keyword search.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/7c3f892b-5dde-4307-a494-f066bed6a024)

I tested for, "pico", "picoctf", "flag", and "flag.txt". From searching for flag.txt I got this file.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/66aa589b-f2f6-442c-8dec-afebb802b0c3)

Based on this the flag is likely in my_folder. When going back to file analysis, and expand directories you can see my_folder at the very bottom.

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/c36533a0-6685-41e6-a9f1-1cb896c93764)

It is inside the root folder which I could have checked at the begining as it is an obvious place to put the flag. The file that was found in the search was the .ash_history in the root folder that captured the commands that they wrote. Before removing flag.txt they moved the file contents to flag.uni.txt with modifications.

This is flag.uni.txt -

![image](https://github.com/noamgariani11/picoCTF-2022-Writeup/assets/91398631/af1f8db9-08e1-4338-b3e1-18a7d441ec60)

At the bottom of the file you can see in the contents of the file is the flag. So now I exported flag.uni.txt into downloads and then moved the txt file into my working directory.

I thought I might have had to delete charaters, but by downloading the file and then using cat to display the contents it just gives the flag.

Flag: ```picoCTF{by73_5urf3r_3497...}```
