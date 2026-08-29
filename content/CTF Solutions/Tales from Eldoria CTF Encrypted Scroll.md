---
title: "Tales from Eldoria CTF: Encrypted Scroll Solution"
draft: false
tags:
  - ReverseEngineering
---
I booted up IDA selecting the executable given to us and was presented with main

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfWdZOR3ajUJlTAFOJ4qkcnSsDqMRYycGjjy6iuBo2ISg4VyCWh_XDhdf_DMNJLa6G2eIhmNhzYrfZjEobnPd1C0XdUV2Kk-NKLl0CwN4e0sKkXfDmncDX1DjY_Dgof2kx0V2j6NQ?key=6sLZ4PoVn4tMbxjRLKRzAnjJ)

The three functions that stood out were anti_debug, display_scroll, and decrypt_message. Function anti_debug is shown below

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdi43d2JRoB4USrNJJII7wHJU52rrM4JhA-msuoQ9WMV-IiOSVSfICKLI09srVbxF1Re79JTT6KaEt-NcCsy8zP-HV9kBXRE1ETdPtVBF7-0dpYDaOE9KfuWH11ligHVuP83UylBA?key=6sLZ4PoVn4tMbxjRLKRzAnjJ)

The anti_debug function does not give any clue as to what the flag is but it has a ptrace function, which is a Unix syscall for tracking another process. This is a common feature for debugging so it makes sense why this is located in the anti_debug function. Below is the function display_scroll

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXezPJxSksl99lpHHqpmnuHYlM_BnKlw8IEJrqfMFMuwjDSQgW6_iq5YEpQ7kApK8eA6VXDq1YeLyjrEOnb5mLSVYqbWWlYv9CI3rmRWek-de7vT5PN6sB3oQ7Q2dSa5ZdiBHoy8?key=6sLZ4PoVn4tMbxjRLKRzAnjJ)

All display_scroll does is print a cryptic message for the user to read when running the executable. Below is the function decrypt_message

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcDDxBmqU_x2otNtEV4aMt0xduzFqD5IGCDxYQ5acMdOXvJAoTX5gnlkF52lhV3MEeFO5yPGsoF8FbXoWDkIT1lqrI_7CKV020MeyiwQuosaIElLnQXYaGoVdcflnnmn2zxyNCT?key=6sLZ4PoVn4tMbxjRLKRzAnjJ)

This function gives me high hopes because I notice that the success and failure strings are located here. The success string is line 12 and to get there, line 11’s condition must be passed. Line 11 is comparing the user’s input with s2, which is set at Line 8 and manipulated at Line 9 and 10. In Line 9 and 10, the for loop is iterating through each character and decrementing each character by 1. Below is a simple python script that will do it for you.  
  
```
encrypted_flag = "IUC|t2nqm4`gm5h`5s2uin4u2d~"  
decrypted_flag = ''.join(chr(ord(c) - 1) for c in input_string)  
print(decrypted_flag)
```
  

Running the script will give you the flag! The output is  
  
`HTB{s1mpl3_fl4g_4r1thm3t1c}`