---
title: Ghiro's Crackme1 Solution
draft: false
tags:
  - ReverseEngineering
---

## Description

  
This is my first crackme, I hope that you enjoy!

The flag format is: `CTF{...}`

## Solution

### Step 1: Analyzing What’s Given

After extracting the crackme, I ran the executable to see what I’m dealing with. The UI shown below appears.  
  
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd0XCXTpv9Tevaumu_CO855VaKL98nfRIgdRS80HPbQI0g4xBkmoEcqgYyTfsdA0J8bFumsCX7T1GdP_Th56yRHd9ARifzBM5DdPv-OBnERfnBJ7e1Lfsz7EVV2K9CXyZTrUBnNWQ?key=x1upplVQ6jc3nxly7BMMnHUn)

When pressing the About key, the pop up shown below appears.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf62L5vQ6Kw9BvNXi2zPCk0MTXWq9FzaVHzcnFVu88S7IVF_J07Ld1eXW19EE9Ll213loFN6Pfpp-Lumc_hn0Ct7rkRafsn4fk7Q1J4aKONm5HlumzM-7hS6hHm68Hfw_c9XADj?key=x1upplVQ6jc3nxly7BMMnHUn)

I then clicked the Check button with an empty field to see what the incorrect pop up message is.


![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcOgAiGLABb7nuXNIVAVYj1cOiGlp-Hnyzwj0UgkLFkebo-XfWjIcXN8ITeisyTDsJHCqOK4wvIvPcgHUPjrg37vucz277u6GxLpKhFy9_0gEtFY7Kb3OGJtNCzP-Z486C8gtlXew?key=x1upplVQ6jc3nxly7BMMnHUn)

After testing all possible inputs, I booted up the terminal and ran the file command to gain more information about the PE file. The output is shown below

`file .\CrackMe1.exe`

`.\CrackMe1.exe: PE32 executable (GUI) Intel 80386 (stripped to external PDB), for MS Windows`

The PE file is PE32 meaning that we will need to run the x32dbg version of x64dbg
### Step 2: x32dbg

I attached the executable with x32dbg and selected the “Find Strings” option to hopefully find the strings I encountered while exploring the UI.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfAqOrCCHcR8DaQv_OfJ0IAh6ZSsXgaOXS3L5SGFUOPylTSvvVjcmgZb9N_6T9UTC-Th2BSOPsVJOKiB5yoSv1KRdHUqyBwQI9zvgi5cQ3f_fNwJq9ROqK6NvrNQFxLJ3IWHw2b0A?key=x1upplVQ6jc3nxly7BMMnHUn)

Not only did I find the strings outputted by the popups, I also found what appears to be the key! It looks promising because it is in the format the description states. I inputted that key in the UI and got the following

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXceNAUcyvOoS2CqjR6qIoIl_9xkK2dPxVlXv_WlgO2_0l5NQ99uL4enOZQ0uNM5ZAeOGr0THPGzWqf6B0tssS5L4VrYqSNp5Firfh91OUK-bRHf-cIHyCaBKYDx9KOBprqd-o98uw?key=x1upplVQ6jc3nxly7BMMnHUn)

The crackme has been cracked!

Solution: `CTF{9110-2324-0502-2034-3454}`