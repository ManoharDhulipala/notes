---
title: PicoCTF2025 RED
draft: false
tags:
  - Forensics
---

## Description

RED, RED, RED, RED

Download the image: [https://challenge-files.picoctf.net/c_verbal_sleep/831307718b34193b288dde31e557484876fb84978b5818e2627e453a54aa9ba6/red.png](https://challenge-files.picoctf.net/c_verbal_sleep/831307718b34193b288dde31e557484876fb84978b5818e2627e453a54aa9ba6/red.png)

Hint #1: The picture seems pure, but is it though?
Hint #2: Red?Ged?Bed?Aed?  
Hint #3: Check whatever Facebook is called now.

## Solution

Visually looking at the image does not help but there could be some metadata that can hold the flag. Metadata is a good area to start since Hint #3 suggests that META (Facebook’s current name) is up to this.

I used the exiftool command in terminal shown below

`exiftool red.png`

Below is the output

  
```

ExifTool Version Number     : 13.00

File Name                   : red.png

Directory                   : .

File Size                   : 796 bytes

File Modification Date/Time : 2025:03:05 22:34:15-05:00

File Access Date/Time       : 2025:05:02 20:25:07-04:00

File Inode Change Date/Time : 2025:05:02 20:25:07-04:00

File Permissions            : -rw-rw-r--

File Type                   : PNG

File Type Extension         : png

MIME Type                   : image/png

Image Width                 : 128

Image Height                : 128

Bit Depth                   : 8

Color Type                  : RGB with Alpha

Compression                 : Deflate/Inflate

Filter                      : Adaptive

Interlace                   : Noninterlaced

Poem                        : Crimson heart, vibrant and bold,.Hearts flutter at your sight..Evenings glow softly red,.Cherries burst with sweet life..Kisses linger with your warmth..Love deep as merlot..Scarlet leaves falling softly,.Bold in every stroke.

Image Size                  : 128x128

Megapixels                  : 0.016
```

  

The metadata reveals a poem, but there is no clue for the flag. I used another command called [zsteg](https://github.com/zed-0xff/zsteg) shown below

`zsteg red.png`

The following is the output

  
```

meta Poem       .. text: "Crimson heart, vibrant and bold,\nHearts flutter at your sight.\nEvenings glow softly red,\nCherries burst with sweet life.\nKisses linger with your warmth.\nLove deep as merlot.\nScarlet leaves falling softly,\nBold in every stroke."                                                                                          

b1,rgba,lsb,xy  .. text: "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ=="                                                                   

b1,rgba,msb,xy  .. file: OpenPGP Public Key

b2,g,lsb,xy     .. text: "ET@UETPETUUT@TUUTD@PDUDDDPE"

b2,rgb,lsb,xy   .. file: OpenPGP Secret Key

b2,bgr,msb,xy   .. file: OpenPGP Public Key

b2,rgba,lsb,xy  .. file: OpenPGP Secret Key

b2,rgba,msb,xy  .. text: "CIkiiiII"

b2,abgr,lsb,xy  .. file: OpenPGP Secret Key

b2,abgr,msb,xy  .. text: "iiiaakikk"

b3,rgba,msb,xy  .. text: "#wb#wp#7p"

b3,abgr,msb,xy  .. text: "7r'wb#7p"

b4,b,lsb,xy     .. file: 0421 Alliant compact executable not stripped
```

The zgets command reveals more information than exiftool. There is a string that resembles base64. 

```
"cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==" 
```

I pasted that in [CyberChef](https://gchq.github.io/CyberChef/), applied a Base 64 decoder and found the flag!  
  
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdmF5tVfXO-X_atJfXbEZjNOZlhfW6nRMOQVFtudBQzX6t_WHttKilprIZTKjmgJbNcYxeBAe5kAW45g7jPD5__KGHSlGsxXhP1qFy6k5Hefk5NQNU7BTGNFNBr34_UAijKMZCjiQ?key=9ZXyIRSdzslviKeU0k9fUjAd)


The solution is  
  
`picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}`