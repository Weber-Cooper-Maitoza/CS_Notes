#### Goals:
- IEEE 754 Floating Point Storage 
- Error detection and correction
- Character Representation
## 2.5 Floating-Point Number Representation:
---
floating-point numbers consist of three parts: 
- a sign bit
- an exponent part (representing the exponent on a power of 2)
- a fractional part (which has sparked considerable debate regarding appropriate terminology).
The term `mantissa` is widely accepted when referring to this fractional part.

==USE THE TERM== "`significand`" to refer to the fractional part of a floating-point number combined with the implied binary point and implied 1 

The number of bits used for the exponent and `significand` depends on whether we would like to optimize for range (more bits in the exponent) or precision (more bits in the `significand`).
![[Pasted image 20230911140340.png]]

17.0 = 0.10001 X 2^5 

\[0]\[00101]\[10001000] = 17.0

\[0] = sign bit
\[00101] = Exponent "5" for 2^5
\[10001000] = `Significand` or 17 base(10)

#### excess- 15 representation:

Any number larger than 15 in the exponent field represents a positive value and Vice Versa.
We use this to be able to represent 0.25 in binary. 

![[Pasted image 20230911144213.png]]

To calculate the value of this number, we would take the exponent field (binary value of 20) and subtract the bias (20 − 4), giving us a “real” exponent of 5, resulting in 0.10001000 × 25.

==Normalization== = the leftmost bit of the `significand` must always be 1.
any model used to represent floating-point numbers ==must treat 0 as a special case==.

![[Pasted image 20230912083705.png]]

### 2.5.2 Floating-Point Arithmetic:
---
Add the following binary numbers as represented in a normalized 14-bit format, using the simple model with a bias of 15.

![[Pasted image 20230912084203.png]]

### Standards:
---
IEEE-754 single-precision standard
![[Pasted image 20230912085507.png]]

### Using `=` on floating points:
---
![[Pasted image 20230912093810.png]]

## IEEE-754 Floating Point:
---
Uses 32 bits
#### How to convert "0.1011" into binary:
---
0.1011 (2): \[0] \[.] \[1] \[0] \[1] \[1]
- 2^-1 = .5 = 0.\[1]011 -> Add .5
- 2^-2 = .25 = 0.1\[0]11 -> don't add .25
- 2^-3 = .125 = 0.10\[1]1 -> Add .125
- 2^-4 = .0625 = 0.101\[1] -> Add .0625
- Add together:
	- .5
	- .125
	- .0625
	- = .6875
#### Converting from Decimal to Binary:
---
-4572.875
- convert from decimal to hex: 4572
	- \[]\[]\[]\[] = 4096, 256, 16, 1
	- \[1] = 4572 / 4096 = 1 (whole number)
	- \[1] = 4572 - 4096 = 476 / 256 = 1
	- \[D] = 220 / 16 = 13 (D)
	- \[C] = 13 * 16 = 208 - 220 = 12 (C)
	- 0x11DC
- convert from hex to binary:
	- \[1]\[1]\[D]\[C]
	- \[1] = \[0001]
	- \[1] = \[0001]
	- \[D(13)] = \[1101]
	- \[C(12)] = \[1100]
	- 0001 | 0001 | 1101 | 1100
- Add on decimal fraction: "0.875"
	- 2^-1 = .5 -> .875 / .5 = 1
	- 2^-2 = .25 -> .875 - .5 = .375 / .250 = 1
	- 2^-3 = .125 -> .375 - .250 = .125 / .125 = 1
	- .111 + 0001 | 0001 | 1101 | 1100 =  0001000111011100.111
- Normalize (move decimal to the furthest left digit and remove zeros):
	- 0001000111011100.111
	- 1.000111011100111 : moved 12 decimal places (Bias = 12)
	- drop leading 1 = .000111011100111
- Find exponent binary:
	- Bias = 12
	- 2^8(bits) - 1 = 127 : Add 12 (Bias) to 127 = 139
	- Convert 139 to Hex then to Binary:
		- 139 (10) = 139 / 16^1 = 8
		- 128 - 139 = 11 = B
		- 0x8B
		- \[8] = \[1000]
		- \[B] = \[1011]
		- 1000 | 1011
- Add Sign, Exponent, and Mantissa
- \[1] \[10001011] \[000111011100111]
- Pad with remaining bits as `0`
- \[1] \[10001011] \[00011101110011100000000]  = -4572.875
- Convert Binary to Hex (Optional):
	- 1100 | 0101 | 1000 | 1110 | 1110 | 0111 | 0000 | 0000
	- 12 | 5 | 8 | 14 | 14 | 7 | 0 | 0
	- 0xC58EE700 =  -4572.875
#### Example:
---
\[1] \[10001011] \[10101101001011000000000]
- \[1] = "-" a negative
- \[10001011] = 12
	- 0x8B = (16^1 * 8) + (16^0 * 11) = 139 - 127 (bias: 127 ((2^8(position) -1) / 2))) = 12
- \[10101101001011000000000] 
	- Add leading "1" = 1.10101101001011000000000
- move decimal 12 times to right = 1101011010010.11
- convert to hex: 0001 | 1010 | 1101 | 0010 | .11
	- 0x1AD2
- convert to decimal:  0x1AD2
	- 1 * 4096 = 4096
	- 10 * 256 = 2560
	- 13 * 16 = 208
	- 2 * 1 = 2
	- add all together = 6866
- convert ".11" to decimal: .11
	- .1 (2) = .5
	- .01 (2) = .25
	- add together: .75
- combine sign, whole numbers, and decimal fractions
	- \[-] \[6866] \[.75] : ==-6866.75==



#### Practice converting HEX 32bit floating point numbers to Decimal:
---
1. C51DD400
- convert to binary
	- \[C] = 12 = \[1100]
	- \[5] = \[0101]
	- \[1] = \[0001]
	- \[D] = 13 = \[1101]
	- \[D] = 13 = \[1101]
	- \[4] = \[0100]
	- \[0] = \[0000]
	- \[0] = \[0000]
	- \[1] \[10001010] \[00111011101010000000000]
	- \[1] = ==negative==
- convert to hex (decimal area):
	- 1000 | 1010 = 0x8A
	- (16 * 8) + (10) = 138
	- 138 - 127 = ==11 Bias==
- Convert Mantissa: 00111011101010000000000
	- un-normalize = 1.00111011101010000000000
	- move decimal point 11 = 100111011101.01
	- convert to Hex: 1001 | 1101 | 1101 .01
		- 0x9DD 
		- convert 0x9DD to decimal: 
			- (9 * 256) + (13 * 16) + (1 * 13) = 2525
		- add .01 (2) = .25
			- 2525.25
		- add negative:
			- -2525.25

2. C49A4400
- 
## 2.6 CHARACTER CODES:
---
#### Binary-coded decimal (BCD):
BCD encodes each digit of a decimal number into a 4-bit binary form.

Digit BCD:
0 = \[0000]
1 = \[0001]
2 = \[0010]
3 = \[0011]
4 = \[0100]
5 = \[0101]
6 = \[0110]
7 = \[0111]
8 = \[1000]
9 = \[1001]
Zones:
unsigned = \[1111]
positive = \[1100]
negative = \[1101]
#### packed decimal format (Packed BDC):
stores 2 digits in 8 bits because 8 bits are standard

+146:
0001 | 0100 | 0110 | 1100:
1. 0001 = 1
2. 0100 = 4
3. 0110 = 6
4. 1100 = +

the sign is encoded at the last 4 bits.

#### Others:
+146 in EBCDIC zoned-decimal format is 11110001 11110100 11000110 (note that the high-order nibble of the last byte is the sign). In ASCII zoned- decimal format, +146 is 00110001 00110100 11000110.

#### Character Encoding:
Extended Binary Coded Decimal Interchange Code (EBCDIC).
American Standard Code for Information Interchange (ASCII).

#### ASCII:
As you can see in Table 2.7, ASCII defines codes for 32 control characters, 10 digits, 52 letters (uppercase and lowercase), 32 special characters (such as $ and #), and the space character. The high-order (eighth) bit was intended to be used for parity.

##### Parity:
the most basic of all error-detection schemes.
>A parity bit is turned “on” or “off” depending on whether the sum of the other bits in the byte is even or odd.

if we decide to use even parity and we are sending an ASCII A, the lower 7 bits are 100 0001. Because the sum of the bits is even, the parity bit would be set to “off ” and we would transmit 0100 0001. Similarly, if we transmit an ASCII C, 100 0011, the parity bit would be set to “on” before we sent the 8-bit byte, 1100 0011. Parity can be used to detect only single-bit errors.


#### Unicode:
16-bit alphabet that is downward compatible with ASCII and the Latin-1 character set.
This is sufficient to provide codes for every written language in the history of civilization.

## 2.7 ERROR DETECTION AND CORRECTION:
---
Parity is able to compensate for multiple bit errors in the same data block.
- FALSE
#### Cyclic Redundancy Check:
---
type of checksum used primarily in data communications that determines whether an error has occurred within a large block or stream of information bytes.

Checksums and CRCs are types of systematic error detection schemes (the error-checking bits are appended to the original information byte.)

The group of error-checking bits is called a syndrome.

How it works:
1. Let the information byte I = 1001011. (Any number of bytes can be used to form a message block.)
    
2. The sender and receiver agree upon an arbitrary binary pattern, say, P = 1011. (Patterns beginning and ending with 1 work best.)
    
3. Shift I to the left by one less than the number of bits in P, giving a new I = 1001011000.
    
4. Using I as a dividend and P as a divisor, perform the modulo 2 division (as shown in Example 2.39). We ignore the quotient and note that the remainder is 100. The remainder is the actual CRC checksum.
    
5. Add the remainder to I, giving the message M: 1001011000 + 100 = 1001011100
    
6. M is decoded and checked by the message receiver using the reverse process. Only now P divides M exactly:
![[Pasted image 20230912102144.png]]
A remainder other than 0 indicates that an error has occurred in the transmission of M.

#### Hamming Codes:
---
==Hamming Codes are able to detect and correct errors.==

Hamming Codes are an adaptation of the concept of parity, whereby error detection and correction capabilities are increased in proportion to the number of parity bits added to an information word.

Hamming codes are used in situations where random errors are likely to occur.

The memory word itself consists of `m bits`, but `r redundant bits` are added to allow for error detection and/or correction. Thus, the final word, called a ==code word==, is an `n-bit` unit containing `m data bits` and `r check bits`.

The smallest Hamming distance found among all pairs of the code words in this code is called the `minimum Hamming distance` for the code.

The `minimum Hamming distance` of a code, often signified by the notation D(min), ==determines its error detecting and correcting capability==.

>to detect k (or fewer) single-bit errors, the code must have a Hamming distance of D(min) = k + 1.


#### Which Error Detection and Correction Scheme is able to compensate for Burst Errors?
- Reed Solomon