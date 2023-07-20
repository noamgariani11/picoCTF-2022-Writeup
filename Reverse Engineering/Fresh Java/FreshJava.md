# Description

Can you get the flag?

Reverse engineer this Java program.

# Solution

```https://artifacts.picoctf.net/c/199/KeygenMe.class```

If you cat the file you can see the flag (it is most recognizable near the end).

```cat KeygenMe.class```

![image](https://user-images.githubusercontent.com/91398631/236709960-11bee629-1b6b-466c-b609-a536e96a22d2.png)

However it seems to be reversed.

Since this is a class file and we know it is a Java progam we can use jd-gui to decompile the file.

```sudo apt install jd-gui```

Then run ```jd-gui``` in the command line.

![image](https://user-images.githubusercontent.com/91398631/236710042-0ce09731-cf30-4be8-87fd-b1263b02d3fa.png)

Once there I used "open file" to open the correct file. This then gave the decompiled Java code, however I'd prefer to view this in the command line so I then saved the file as "KeygenMe.java" in the correct directory.

![image](https://user-images.githubusercontent.com/91398631/236710106-ccd36b73-68ec-4e70-8931-8d49cc4711a1.png)

In the Java file we can see the same thing that it is looking at the flag charater by charater in reverse.

![image](https://user-images.githubusercontent.com/91398631/236710224-50fa0a2b-c4d3-487a-8c73-08ca6cd1e6e4.png)

Since every line there is a part of the flag there is "str.charAt()", I used grep to look for "str.char". 

```cat KeygenMe.java | grep str.char```

![image](https://user-images.githubusercontent.com/91398631/236710481-d7bc6bd0-8989-4d42-8906-ccfb129124af.png)

Now to get just the letters themselves I used cut to look at the ' delimiter and the second field.

![image](https://user-images.githubusercontent.com/91398631/236710513-6a3ff906-5c0b-4e3c-a730-036d360b00d0.png)

```cat KeygenMe.java | grep str.char | cut -d "'" -f2```

Each charater was on a newline so I used tr to look at the \n (newline) delimiter and delete it.

![image](https://user-images.githubusercontent.com/91398631/236710558-b427aa98-5a78-47ef-8a62-cf3a1d883bed.png)

Now I used "rev" to reverse the output.

```cat KeygenMe.java | grep str.char | cut -d "'" -f2 | tr -d "\n" | rev```

This gives the flag successfully.

Flag: ```picoCTF{700l1ng_r3qu1r3d_2bf...}```
