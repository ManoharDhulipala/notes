---
title: PicoCTF2025 Pie Time
draft: false
tags:
  - ReverseEngineering
---

## Understanding the Problem

  
Below is the problem’s description. The user will have a different netcat server connection.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfbpPT_MQ1pu8MnpIFV1hjqIkSEkMLHBBNHcZ0AuSLR9xTKKUkaPuzcvtauW0Bpl8hQFKJEG28-82pFkkaa_lGK6FABAkgsEm9IyhcGVxpL7p1XmgKZC9c6FPDKi85Snthgf_o3eQ?key=qpw0t2Pf_esNPEsxVgKDgFWz)

The source code is the following.

```
#include <stdio.h>  
#include <stdlib.h>  
#include <signal.h>  
#include <unistd.h>  
  
void segfault_handler() {  
  printf("Segfault Occurred, incorrect address.\n");  
  exit(0);  
}  
  
int win() {  
  FILE *fptr;  
  char c;  
  
  printf("You won!\n");  
  // Open file  
  fptr = fopen("flag.txt", "r");  
  if (fptr == NULL)  
  {  
  printf("Cannot open file.\n");  
  exit(0);  
  }  
  
  // Read contents from file  
  c = fgetc(fptr);  
  while (c != EOF)  
  {  
  printf ("%c", c);  
  c = fgetc(fptr);  
  }  
  
  printf("\n");  
  fclose(fptr);  
}  
  
int main() {  
  signal(SIGSEGV, segfault_handler);  
  setvbuf(stdout, NULL, _IONBF, 0); // _IONBF = Unbuffered  
  
  printf("Address of main: %p\n", &main);  
  
  unsigned long val;  
  printf("Enter the address to jump to, ex => 0x12345: ");  
  scanf("%lx", &val);  
  printf("Your input: %lx\n", val);  
  
  void (*foo)(void) = (void (*)())val;  
  foo();  
}
```

The source code has three functions: main(), segfault_handler(), and win(). main() is the first function the user will interact with and it requests a memory address value from the user. The function also prints the current address of main(). The inputted address is read with the scanf function. That scanned address is then type casted as a function foo() and is called in the last line.

If foo() does not exist because the user inputs an incorrect address, the segfault_handler() is called and informs the user that an incorrect address was inputted.

The win() function’s address appears to be the one that the user wants to find because it outputs the flag. The goal is to then find the address of win() and we are given the address of main.

## Solution

gdb is the optimal choice rather than using a robust decompiler like Ghidra or IDA because all we care about is the address location of win and main.

We will need to download the binary file given to us and run the command

`gdb vuln`

This command will initialize the debugger on the vuln binary. To look at the assembly of main, the following command is called

`gdb disass main`

disass is short is [disassemble](https://visualgdb.com/gdbreference/commands/disassemble), which reveals the assembly of the binary. The second input, main, requests the assembly values of main specifically. Below is the output

  

```
0x000000000000133d <+0>: endbr64

0x0000000000001341 <+4>: push   %rbp

0x0000000000001342 <+5>: mov %rsp,%rbp

0x0000000000001345 <+8>: sub $0x20,%rsp

0x0000000000001349 <+12>: mov %fs:0x28,%rax

0x0000000000001352 <+21>: mov %rax,-0x8(%rbp)
```

This is the beginning of main() and the rest is not shown because it is irrelevant to the problem. The command below will show the assembly of win()


```
0x00000000000012a7 <+0>: endbr64

0x00000000000012ab <+4>: push   %rbp

0x00000000000012ac <+5>: mov %rsp,%rbp

0x00000000000012af <+8>: sub $0x10,%rsp

0x00000000000012b3 <+12>: lea 0xd74(%rip),%rdi    # 0x202e
```


Now that we know the beginning addresses of win and main, we can compute the difference of the address and find the offset between main and win. Once the offset is acquired, that value will be added to the main address given from the netcat server where the flag is located. The addresses we will find the difference of are highlighted in light blue.

`0x0…0133d - 0x0…012a7 = 0x96`

Whatever address value is given by main, we will need to subtract 0x96 from it and that should hit the win() function giving the flag.

  
  
  

Running the netcat command gives the following prompt

  

Address of main: `0x59b1aed7833d`

Enter the address to jump to, `ex => 0x12345`:

main()’s address on the server is given and subtracting 0x96 from it is 0x59b1aed782a7.

  

Inputting that value, gives the solution!

  


```
Address of main: 0x59b1aed7833d
Enter the address to jump to, ex => 0x12345: 0x59b1aed782a7
Your input: 59b1aed782a7
You won!
picoCTF{b4s1c_p051t10n_1nd3p3nd3nc3_ecb96bdd}
```

  
  

Here is a python script that calculated the difference of main()’s address and the offset

```
hex_value1 = "59B1AED7833D"  
hex_value2 = "96"  
  
int_value1 = int(hex_value1, 16)  
int_value2 = int(hex_value2, 16)  
  
difference = int_value1 - int_value2  
  
hex_difference = hex(difference)  
  
print(f"The difference between {hex_value1} and {hex_value2} is: {hex_difference}")
```

