# Open Serial Binary Protocol (SBP) specification

## Protocol frame structure

SYNC1 | SYNC2 | LENGTH | MODE | ID | PAYLOAD | CHECK1 | CHECK2|
|----------|----------|----------|----------|----------|----------|----------|----------|
U1 | U1 | U1 | U1 | U1 | BYTE[LENGTH] | U1 | U1 |
0xBB | 0x55 | 0 … 128 | 0 … 255 | 1 … 255 | — | 0 … 255 | 0 … 255 |


## Checksum
The checksum algorithm used is the Fletcher-16.

Example source code for calculating the checksum:
```
uint8_t CHECK1 = 0;
uint8_t CHECK2 = 0;
void CheckSumUpdate(uint8_t byte) {
	CHECK1 += byte;
	CHECK2 += CHECK1;
}
```

## Number Formats
- Multi-byte values are ordered in Little Endian format
- Floating point values are transmitted in IEEE754 single or double precision
- bit-field in LSB format
