## Chapter 1 - intro
---
ISA = Instruction Set Architecture
interface between software and hardware

#### What is a computer?
1. CPU - handles instructions
2. Memory 
3. I/O
Developed by Charles Babbage

#### Principle of Equivalence Between Hardware and Software:
any task that can be completed with software can be completed by hardware and vice versa.
because of ISA

kb = base 10 bits 
KB = base 2 bytes

bytes = 8 bits

#### Mores Law:
transisters double every 18-24 months

#### Von Neumann Arch.
![[Pasted image 20231027091556.png]]
1. CPU 
	1. controll unit 
	2. ALU - Arithmetic Logic Unit
	3. Registers
2. Memory, RAM, I/O
3. Sequintial Instructions
4. Single pathway between CPU and RAM (Von Neumann Bottle Neck)
5. Execution Cycle
6. 
	1. Fetch 
	2. Decode
	3. Execute (repeate)

## Chapter 2 - Data Representation in Computer Systems
---
An 8-bit Byte can be divided into to 4-bit intervals called "==Nibbles==".
==1111== 1111 : the high order nibble
1111 ==1111== : the low order nibble
#### 2.2 POSITIONAL NUMBERING SYSTEMS:
---
The general idea behind positional numbering systems is that a numeric value is represented through increasing powers of a ==radix== (or base).

## Conversions Between Bases:

#### Decimal to Binary:
---
| 128 : 64 : 32 : 16 | 8 : 4 : 2 : 1 |
2^n = nth position starting at 0

387(10) => (2)?
2 % 387 = 1
2 % 193 = 1
2 % 96 = 0
2 % 48 = 0
2 % 24 = 0
2 % 12 = 0
2 % 6 = 0
2 % 3 = 1
2 % 1 = 1

387(10) = 0001|1000|0011 (2)

#### Binary to Hex:
---
0001|1000|0011 (2) = (16) ?
0001 | 1000 | 0011
| 8 : 4 : 2 : 1 |
0001 = 0x1
1000 = 0x8
0011 = 0x3
0001|1000|0011 (2) = 183(16)


#### Decimal to Hex:
---
387 (10)
- set up nibbles: \[] \[] \[]
- 16^2 = 256 , 16^1 = 16 , 16^0 = 1
- 387 / 256 = 1.5 = \[1] \[] \[] 
- 387 - (256 * 1) = 131 / 16 = 8.18 = \[1] \[8] \[]
- 131 - (8 * 16) = 3 / 1 = 3 = \[1] \[8] \[3]
- ==0x183==

#### Hex to Decimal:
---
0xAF94
- 16^3 = 4096 * 10 (A) = 40960
- 16^2 = 256 * 15 (F) = 3840
- 16^1 = 16 * 9 = 144
- 16^0 = 1 * 4 = 4
- Add all together:
	- 40960 
	- 3840
	- 144
	- 4
	- + = 44948