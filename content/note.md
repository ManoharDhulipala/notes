---
title: Pointer Basics
draft: false
tags:
  - example-tag
---
 
The notes will be from the perspective of a reverse engineer.

Example Native Data Types: int, float, double, unsigned int, etc.

When writing code, you will declare a variable that has a native data type. When compiled, that variable will be assigned an address on memory. The address will contain the value of the variable.

A **pointer** is a variable that contains an address rather than a value. For example

```
DWORD* pdwValue
```

pdwValue is an address value that hold a DWORD value. The statement above promises that the address holds a DWORD.

When a pointer is defined, the actual value is **not** allocated. So when the line above is compiled, the memory will only make space for the address.

There can be double or n pointers. A double pointer points to an address that points to another address that points to the native data type.

How do we make our pointers point to another variable?

```
DWORD dwValue;
dwValue = 10;
&dwValue;
```

The first two lines above initializes a variable and sets it to 10. At compile time, there will be an address value given that holds the value 10. The last line gets the address of the variable.

```
DWORD *pdwValue = &dwValue
```

Looking at the line above, a pointer pdwValue is initialized and it is set to the address of dwValue. This is valid because dwValue is a DWORD, which matches the initialization of pdwValue.

### Example

```
DWORD* pdwValue
DWORD  dwValue
pdwValue = &dwValue
*pdwValue = foo
```

Line 1 initializes variable that holds an address that can contain a dword
Line 2 initializes an empty DWORD value
Line 3 stores the address of the empty DWORD value to the line 1 variable
Line 4 accesses the value of the address intialized in line 1 and set in line 3. Below will show outputs of the variables. This is the process of dereferencing.

```
print("%d", pdwValue) //outputs an address
print("%d", *pdwValue) //outputs foo
```

Instead of having a * denoting an address, a bracket is used instead. For example:

```
mov eax, [epb-8]
```

The EPB register stores an address and the brackets mean that it is getting the value stored at the address. With that value stored in the address in the EPB register, move that value into the EAX register.

