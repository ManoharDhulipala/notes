---
title: Analyzing a Portable Executable File
draft: false
tags:
  - Forensics
  - ReverseEngineering
---
## Overview


I had the opportunity to present at the local DC256 chapter on analyzing the Portable Executable Format.

![[Pasted image 20260829162343.png|300]]

![[Pasted image 20260829163358.png|300]]

I went into great depth analyzing the portable executable file structure by walking through the many headers and sections alongside an example. Here is a [link](https://docs.google.com/presentation/d/1GjOnt0L1X7uYIlKC4wrnkSQ6nLa4wBwOqiVj89ovRmk/edit?usp=sharing) to the slides I presented with as well as the [examples](https://github.com/ManoharDhulipala/PE_Examples). Below are qualities I wanted the audience to notice when analyzing the examples.

## Examples

Reverse engineers need a strong understanding of the Portable Executable File Format in order to not get tricked when malware authors manipulate certain sections. For example,  the `exercise.exe` executable does not contain your typing DOS Stub. Below is a screenshot of what happens when you run that file with the [neilb](https://www.neilb.net/doswasmx/) DOS WASM app.

![[Pasted image 20260829164115.png|600]]

Despite the DOS Stub being manipulated, the program will still function and that is because the DOS Stub is not integral for the Windows Operating System to execute this file.

Another common value malware authors manipulate is the time date stamp. When the portable executable is created, the time date stamp notes at what time it was created. This can be easily manipulated with a hex editor. Below shows the time date stamp saved in the executable using Detect it Easy.

![[Pasted image 20260829170501.png|600]]

Even with a manipulated timestamp, the program is still functional.

These curveballs are implemented to throw off reverse engineers and to avoid them, a strong fundamental understanding of portable executables must be developed.

