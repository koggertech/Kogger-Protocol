# Open Serial Binary Protocol (SBP) specification

## Protocol frame structure

## Checksum
The checksum algorithm used is the Fletcher-16.
Example source code for calculating the checksum:
uint8_t CHECK1 = 0;
uint8_t CHECK2 = 0;

void CheckSumUpdate(uint8_t byte) {
	CHECK1 += byte;
	CHECK2 += CHECK1;
}

## Number Formats
All multi-byte values are ordered in Little Endian format.
All floating point values are transmitted in IEEE754 single or double precision. 
All bit-field in LSB format.
