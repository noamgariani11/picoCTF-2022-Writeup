# Description

A second message has come in the mail, and it seems almost <br>
identical to the first one. Maybe the same thing will work again. <br>
Download the message here.

# Solution

```wget https://artifacts.picoctf.net/c/182/message.txt```

Cipher text:

SYTe (eakdy tkd sjbyndr yar thjm) jdr j yobr kt skxbnyrd ersndzyo skxbryzyzkc. Skcyreyjcye jdr bdrercyrq gzya j ery kt sajhhrcmre gazsa yrey yarzd sdrjyzwzyo, yrsaczsjh (jcq mkkmhzcm) evzhhe, jcq bdklhrx-ekhwzcm jlzhzyo. Sajhhrcmre nenjhho skwrd j cnxlrd kt sjyrmkdzre, jcq garc ekhwrq, rjsa ozrhqe j eydzcm (sjhhrq j thjm) gazsa ze enlxzyyrq yk jc kchzcr eskdzcm erdwzsr. SYTe jdr j mdrjy gjo yk hrjdc j gzqr jddjo kt skxbnyrd ersndzyo evzhhe zc j ejtr, hrmjh rcwzdkcxrcy, jcq jdr akeyrq jcq bhjorq lo xjco ersndzyo mdknbe jdkncq yar gkdhq tkd tnc jcq bdjsyzsr. Tkd yaze bdklhrx, yar thjm ze: bzskSYT{TD3UN3CSO_4774SV5_4D3_S001_7JJ384LS}

This time there was no key provided and in the hint a frequency analysis attack was alluded to. So I put the cipher text into [quipqiup](https://quipqiup.com/) and ran it and it just gave the flag correctly at the end.

Flag: ```picoCTF{FR3QU3NCY_4774CK5_4R3_C001_7AA384BC}```
