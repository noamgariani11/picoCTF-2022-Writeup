# Description

Download this image file and find the flag.

Download image file

# Solution

```wget https://artifacts.picoctf.net/c/101/drawing.flag.svg```

First I opened the image to try to "enhance" and see if there was a flag and there wasn't. Then I ran ```strings drawing.flag.svg``` and saw the flag.

![image](https://user-images.githubusercontent.com/91398631/229652482-8eed0430-eef8-4246-a326-8ddf8318a1ed.png)

Now I could just copy paste the flag or I could try to make a script to get the flag from the output.

I first took only the data after >" with grep. \" to escape the " charater. 

```strings drawing.flag.svg | grep "\">"```

![image](https://user-images.githubusercontent.com/91398631/229652676-ffa079f7-f468-41f2-9143-8fba174b47c8.png)

Now I used cut to get rid of the first part. "-d" is for the delimeter which in this case is ">" and -f2 is to keep the second feild.

```strings drawing.flag.svg | grep "\">" | cut -d ">" -f2```

![image](https://user-images.githubusercontent.com/91398631/229652860-b932e1c5-d90c-4380-92a2-8e758c6eb10e.png)

Now to get rid of the right side it's the same thing but a different delimeter "<" and -f1 for the first field.

```strings drawing.flag.svg | grep "\">" | cut -d ">" -f2 | cut -d "<" -f1```

![image](https://user-images.githubusercontent.com/91398631/229652939-5383ac64-17ce-457e-8c21-27892254b6ce.png)

Now to get rid of all of the empty lines and new lines use tr with the \n delimeter.

```strings drawing.flag.svg | grep "\">" | cut -d ">" -f2 | cut -d "<" -f1 | tr -d "\n"```

![image](https://user-images.githubusercontent.com/91398631/229653080-1732f661-a117-48b7-941e-27f3130a551d.png)

Now it's basically the flag but with spaces in between every letter. That's easily fixed with tr again but with the delimeter being a space " ".

```strings drawing.flag.svg | grep "\">" | cut -d ">" -f2 | cut -d "<" -f1 | tr -d "\n" | tr -d " "```

![image](https://user-images.githubusercontent.com/91398631/229653151-c3bea777-4f0a-4c8b-967a-e30bef5463d4.png)

Flag: ```picoCTF{3nh4nc3d_24374675}```
