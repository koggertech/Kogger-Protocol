# Open Serial Binary Protocol (SBP) specification

## Protocol frame structure

SYNC1 | SYNC2 | LENGTH | MODE | ID | PAYLOAD | CHECK1 | CHECK2|
|----------|----------|----------|----------|----------|----------|----------|----------|
U1 | U1 | U1 | U1 | U1 | BYTE[LENGTH] | U1 | U1 |
0xBB | 0x55 | 0 … 128 | 0 … 255 | 1 … 255 | — | 0 … 255 | 0 … 255 |

### MODE
Name | Bits | Description
|----------|----------|----------|
TYPE | 0:2 bit | Field defines the type and purpose of the data
VERSION | 3:5 bit | Field defines the data version
MARK | 6 bit | Set by the host and reset when the device reboots. Used only for direction of device-host
RESPONSE | 7 bit | Request response to the command. Used only for direction of host-device

### TYPE of MODE
TYPE | Value | Description
|----------|----------|----------|
RSERVED | 0 | Reserved
CONFIRM | 1 | Confirmation
SETTING | 2 | Setting parameters
GETTING | 3 | Request data
CONTENT | 4 | Content of data
ACTION | 5 | Action request
REACTION | 6 | Reaction on action request
RSERVED | 7 | Reserved

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

Name | Type | Size (Bytes) | Range
|----------|----------|----------|----------|
S1 | int8_t | 1 | -128 ... 127 
U1 | uint8_t | 1 | 0 … 255
S2 | int16_t | 2 | -32768 … 32767
U2 | uint16_t | 2 | 0 … 65535
S4 | int32_t | 4 | -2'147'483'648  ... 2'147'483'647 
U4 | uint32_t | 4 | 0 … 4'294'967'295
F4 | float | 4 | -1*2^+127 ... 2^+127 
D8 | double | 8 | -1*2^+1023 ... 2^+1023 
