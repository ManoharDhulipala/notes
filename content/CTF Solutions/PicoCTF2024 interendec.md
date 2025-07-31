---
title: PicoCTF2024 interendec
draft: false
tags:
---
## Description

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe2kDe90aoAdvMHG6hAIUk5bMBViczNlK63FkCJ1KpKsfqHjThn_AfdC9soq1htJ1Q-uqXSHST8zCtnib16kPdIrxSXXSeWl9ylC9g8SoS_ekRfSio7Op_mKAArhWp0eLPDtdbZxw?key=5UPFpHapJWyASzFJ7JYv6W5I)

File: [https://artifacts.picoctf.net/c_titan/108/enc_flag](https://artifacts.picoctf.net/c_titan/108/enc_flag)
## Solution

The file contains the following ciphertext

`YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclgyZzBOMm8yYXpZNWZRPT0nCg==`

The ciphertext resembles base64 so on CyberChef, I decoded the base 64 and the output is the following

`b'd3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrX2g0N2o2azY5fQ=='`

I removed the byte notation and re-ran the base 64 decoder giving the following output

`wpjvJAM{jhlzhy_k3jy9wa3k_h47j6k69}`

The structure of the ciphertext resembles the flag with the curly braces and that the number of characters before the { brace matches the number of characters for picoctf. I tested the Caesar cipher on it and found the flag! [Here](https://samsclass.info/141/proj/C107.htm) is a link that explains how to implement the Caesar cipher on CyberChef.

`picoCTF{caesar_d3cr9pt3d_a47c6d69}`

Below is the Cyber Chef recipe that converts the ciphertext directly to plaintext.  
  
[Cyber Chef Recipe](https://gchq.github.io/CyberChef/#recipe=From_Base64\('A-Za-z0-9%2B/%3D',true,false\)Drop_bytes\(0,2,false\)Drop_bytes\(-1,-1,false\)From_Base64\('A-Za-z0-9%2B/%3D',true,false\)ROT13\(true,true,false,19\)&input=WWlka00wSnhaR3R3UWxSWWRIRmhSM2cyWVVoc1ptRjZUbkZsVkd3eldWUk9jbGd5WnpCT01tOHlZWHBaTldaUlBUMG5DZz09&oenc=65001)