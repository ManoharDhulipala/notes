---
title: Zenton's Crack Me For Beginners
draft: false
tags:
  - ReverseEngineering
---
After extracting the file, I ran the [strings](https://learn.microsoft.com/en-us/sysinternals/downloads/strings) command on the executable, which outputs all the strings values in the PE file. The output revealed certain strings that were out of the ordinary shown below.

```
Press Enter to exit...

secret123

Enter the password:

Password correct! Access granted.

Incorrect password!
```

The strings above suggest that the user will need to input a password and once the correct one is submitted, the crackme is solved. Otherwise, the incorrect password prompt is outputted

In addition, secret123 jumps out to me since that is normally not found in a PE file. I booted up [IDA](https://hex-rays.com/ida-free), searched for the `Enter the password: ` string, and landed on function sub_140014B90:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdRffTo9Skl7tJyCLGeWUqV30OYjD2bxNpRxfZn4X8u0sofLpYUXgI8K9ZkyrEddt40a-C6gcJP5B9nGJ1SZsTiDFzVilqw5hFPvF32Ow9Hdap9k1zhDUMxCW6q0PGynkKg_23IpA?key=x6_0G6xcEjMQjol5h4yga5aD)

Looking at Line 16 above, the crackme asks the user to enter their password, and that input is passed to the `sub_14001114A` function on Line 18. This function is part of a conditional and if the function outputs a True, the `“Password correct! Access granted!”` prompt is outputted on Line 19. Otherwise, the code will jump to Line 20 and output the `“Incorrect Password!”` prompt. Therefore, the goal is to have function `sub_14001114A` return a true value.  Below is the disassembled code for `sub_14001114A`.  
  
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdcE6PgDWSuXyapWHdPYIlC-a4u-bEZf3QFymag5nhopzsznUPEtMXxkHCAW42bjE1V97BcHT1hlPc5KYrvQjm_UJmXI5bESCSA0Jsyk6h7u_mhss8AjspOuPBQwC-x7-EiK1xdYQ?key=x6_0G6xcEjMQjol5h4yga5aD)

  
`sub_14001114A` returns function `sub_140014860`. The user’s password input is passed to that function and its disassembled code is shown below

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcqM9JceC1fIZRZODep5nCKHZySeaBGXETAGFHH9020-Dk68R8rJeZcfPoOMcBvcEnbWJnKtw4KZYzso_DKMNX7la3IAJPvfk-jupsBf_GMNTGpJ6NYwghYjEf_TIUAXKzguGx8iA?key=x6_0G6xcEjMQjol5h4yga5aD)

The user’s inputted password is represented as `a1`.  On line 18, `Str2` is set to `“secret123”`, which we found with the strings command. Line 19 compares the user’s inputted password with `“secret123”`. If they match, the output is 1 and is stored in the `v8` variable. Line 20 sets the `v8` value to `v3` and `v3` is returned on Line 22. Therefore, if the user’s input matches `“secret123”`, function `sub_140014860` returns 1 or true. We want the function to return a true value to access the `“Password correct! Access granted!”` prompt in `sub_140014B90` (first image)

Below is the command prompt testing whether typing `“secret123”` is the correct answer.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeUfVKjIXB1OLyOVxbkdR4ipqP-M04Ko_Mk2-T5mE7x8Zm3XmZhdobU3N1ltNTtIbvZXMdhhufpYG6JVNt3q4Ru0gklVIBsGIJaQQOcuN45Wqz652AxWH5Q1N3VmJoHUU59JjUB9g?key=x6_0G6xcEjMQjol5h4yga5aD)  
  
`“secret123”` is the correct password and the crackme has been cracked!