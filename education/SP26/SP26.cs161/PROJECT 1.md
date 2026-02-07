# Question 1 writeup
eip → 0xffffd98c 
- saved eip → RIP function
- + 4 = 0xffffd990
edp → 0xffffd988
- saved edp → SFP function

# Question 2 writeup
saved eip → 0xffffd93c
saved edp → 0xffffd938

## Main Idea
The code is vulnerable because integer overflow
![[Screenshot 2026-02-06 at 3.20.31 PM.png]]
## Magic Number
We first determined
![[Screenshot 2026-02-06 at 3.20.09 PM.png]]
## Exploit Structure
Here is the stack diagram

Read arguments right to left
RIP (return instruction pointer) main ← saves code location
SFP (saved framed pointer) main ← top of frame
execute function/code
- local variables

then repeat if call new function

![[Screenshot 2026-02-06 at 4.09.17 PM.png]]
## Exploit GDB Output 
When we ran GDB

# Question 3 writeup

## Main Idea

RIP main
SFP main
Canary main

RIP dehexify ← 0xffffd96c + 4 = 0xffffd970: 0x08049341
SFP dehexify ← 0xffffd978
Canary dexehify ← 0xa4602e87 (0x6d708d28) ← changes      0x0804d020
buffer ← 0x00000000      0x00000000      0xffffdfe1      0x0804cfe8
answer ← 
i ← 4 bytes
j ← 4 bytes


# Question 4 writeup
buf ← 0xffffd8b0