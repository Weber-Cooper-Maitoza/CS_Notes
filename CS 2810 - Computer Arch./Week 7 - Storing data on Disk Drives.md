## Interrupt Vector Table Decoding:
---
![[Pasted image 20231010104152.png]]
==Little endian Format== - Order of bytes are reversed. (important for "segment offset notation")

Example: ==For Interrupt 11H== (11H - 'H' is a way to represent Hex notation)

#### Steps: interrupt (11H):
1. Multiply (11H) by 4: 0x11 \* 0x04 = 0x44 or 44H
2. go to ==0040== spot in memory table (hexdump) (==4==4H)
	1. 0000:0000, 0000:0010, 0000:0020, 0000:0030, ==0000:0040==
3. move over ==4 bytes== (4==4==H)
	1. 0000:0040 09 00 A9 0B ==4D F8 00 F0==-41 F8 00 F0 10 05 51 02
4. ==Reverse 4 bytes== because of Little endian Format (order of bytes are reversed)
	1. 4D F8 00 F0 -> ==F0 00  F8 4D==
5. Convert to a ==Segment Offset Address== (F0 00 F8 4D)
	1. F0 00 F8 4D -> ==F000:F84D== (F000 - ==Segment==) (F84D - ==Offset==)
6. For 16 bit arch, need to convert ==Segment== to 20 bit notation (add 0x00000 to segment)
	1. 0xF000 + 0x00000 = 0xF000==0== -> F000==0==:F84D
7. ==ADD Segment and offset== together to get ==20 bit address==
	1. 0xF0000 + 0xF84D = 0xFF84D -> address ==FF84D==

#### Example (07H):
1. 0x07 \* 0x04 = 0x1C or ==1CH==
2. 0000:==0010== (==1==CH)
3. 0000:0010 65 04 70 00 54 FF 00 F0-4C E1 00 F0 ==6F EF 00 F0== (1==C==H)
4. reverse: F0 00 EF 6F
5. F000:EF6F
6. convert to 20 bit notation: F0000:EF6F
7. Add: FEF6F

#### Example (1BH):
1. 0x1B \* 0x04 
	1. 0x1B = 27
	2. 27 \* 4 = 108
	3. 108 / 16 = 6
	4. 108-96 = C
	5. 0x6C
2. 04 06 E3 D4 (==6C==H)
3. D4E3:0604
4. D4E30:0604
5. add 
	1. 0xD4E30  
	2. +0x0604
	3. D5434

## Fat-16 Boot Sector:
---
![[Pasted image 20231010120754.png]]

"Number of bytes per sector?"
- found in boot sector ==0BH== in ==two bytes== (00 02 = 0200)
- convert to decimal: 0200 = (256\*2 = 512) ==512 bytes per sector==

"Find volume serial number?"
- found in ==27H== in ==four bytes==
- D4 C3 B2 A1 = ==A1B2-C3D4==

## Root Area Decoding:
---
![[Pasted image 20231011094140.png]]![[Pasted image 20231011094202.png]]

C6BD -> BD C6
1011 1101 1100 0110
Hour = left 5 bits : 1 0111 = 23 = 11
Minutes = middle 6 bits :10 1110 = 46
Seconds = right 5 bits : 0 0110 = 6
11:46:12


Date:
44 23 -> 23 44
23 44 -> 0010 0011 0100 0100
year 1980 + left 7 bits : 001 0001 -> 17 + 1980 = 1997
month middle 4 bits: 1010 = 10
day right 5 bits : 0 0100 = 4

Starting cluster:
42 02 -> ==0242H==

