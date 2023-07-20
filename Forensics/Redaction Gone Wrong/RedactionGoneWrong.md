# Description

Now you DON’T see me. <br>
This report has some critical data in it, some of which have <br>
been redacted correctly, while some were not. Can you find <br>
an important key that was not redacted properly?

# Solution

```https://artifacts.picoctf.net/c/84/Financial_Report_for_ABC_Labs.pdf```

I first used pdftotext (you can get with ```sudo apt-get install -y xpdf```).

```pdftotext Financial_Report_for_ABC_Labs.pdf```

This created Financial_Report_for_ABC_Labs.txt which when you cat the contents (cat Financial_Report_for_ABC_Labs.txt) then you see the flag.

```cat Financial_Report_for_ABC_Labs.txt | grep pico```

If you pipe grep with pico then you will get the flag just on that line.

Also if you want you can do ```open Financial_Report_for_ABC_Labs.pdf``` and just highlight the blacked out text and it will show you the flag.

Flag: ```picoCTF{C4n_Y0u_S33_m3_f...}```
