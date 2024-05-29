#### Signed Magnitude Representation:
an 8-bit word: 
−1 would be represented as `10000001` 
+1 as `00000001`

7 bits can be used for the actual representation of the magnitude of the number.

for a signed 8-bit number can have a range between -127 to 127 because it can only use 7 bits.

##### signed-magnitude arithmetic:
![[Pasted image 20230906191420.png]]

if the 7th bit needs to carry into the 8th bit, it cannot happen. Results are `Overflow`.

![[Pasted image 20230906191617.png]]

##### DABBLING ON THE DOUBLE:
a way to convert between binary to decimal 

## Complement Systems:
---

#### One's Complement:
One's complement of 2469 is 9999 - 2469 = 753.

the one’s complement of 01012 is 11112 − 0101 = 1010.

nothing more than switching all of the 1s with 0s and vice versa.

![[Pasted image 20230907085421.png]]
![[Pasted image 20230907085623.png]]

#### Two’s Complement:
two’s complement is nothing more than ==one’s complement incremented by 1==.

two’s complement of a binary number, simply flip bits and add 1.

Converting a negative number to Binary: 11110111 (2) 
- flip bits: 00001000
- then add 1: 00001001
- keep (-): - (00001001)
- conclude: -9

## Converting 16bitSI (HEX) to Binary:
1. Is the digit negative?
	if left most Hex value is 8, 9, A, B, C, D, E, F then it is NEGATIVE.
	POSITIVE: 0-7
2. Convert to Binary:
	2BA6 = 0010 | 1011 | 1010 | 0110
3. Flip Bits if negative:
	F1BC = 1111 | 0001 | 1011 | 1100 => 0000 | 1110 | 0100 | 0011
4. ADD ONE:
	 0000 | 1110 | 0100 | 0011 + 1 => 0000 | 1110 | 0100 | 0100
5. Convert to Decimal:
	0000 = 0 hex
	1110 = E hex
	0100 = 4 hex
	0100 = 4 hex
	![[Pasted image 20230907100313.png]]
	0 * 16^3 = 0
	E (14) * 16^2 = 14 * 256 = 3584
	4 * 16^1 = 64
	4 * 16^0 = 4
	0 + 3584 + 64 + 4 = 3652

## Converting Binary to 16bitSI:
-10256
1. Convert 10256 to binary:
	0010 | 1000 | 0001 | 0000
2. Flip Bits if Negative:
	1101 | 0111 | 1110 | 1111
3. ADD ONE:
	1101 | 0111 | 1110 | 1111 => 1101 | 0111 | 1111 | 0000

1101 | 0111 | 1111 | 0000 = -10256




==The smallest signed 16-bit number is -32768 and the largest is 32767==

==2^16 /2==