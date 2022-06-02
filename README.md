# Wisblock RAK4631_Blowfish

Based on Bruce Schneier's code, see [this page](https://www.schneier.com/books/applied-cryptography-source/).

```c
// blowfish.h interface file for blowfish.cpp
// _THE BLOWFISH ENCRYPTION ALGORITHM_
// by Bruce Schneier
// Revised code--3/20/94
// Converted to C++ class 5/96, Jim Conger
```

Sample code is easy to understand I think, as the C++ class is pretty clean.

```c
  CBlowFish bf;
  BYTE plain[256];
  BYTE encrypted[256];
  BYTE decrypted[256];
  BYTE myKey[17] = "YELLOW SUBMARINE";
  Serial.println("\nmyKey");
  hexDump(myKey, 16);
  bf.Initialize(myKey, 16);
  for (int i = 0; i < 256; i++) plain[i] = i;
  Serial.println("\nplain");
  hexDump(plain, 256);
  bf.Encode(plain, encrypted, 256);
  Serial.println("\nEecrypted:");
  hexDump(encrypted, 256);
  bf.Decode(encrypted, decrypted, 256);
  Serial.println("\nDecrypted:");
  hexDump(decrypted, 256);
```

## Port to other devices

### Comment out nRF52-specific code

`// #include <Adafruit_TinyUSB.h>`

### Move data arrays to `PROGMEM`

When compiling for a smaller device like the Uno.

```c
const PROGMEM DWORD bf_P[NPASS + 2]  = {
  0x243f6a88, 0x85a308d3, 0x13198a2e, 0x03707344,
  0xa4093822, 0x299f31d0, 0x082efa98, 0xec4e6c89,
  0x452821e6, 0x38d01377, 0xbe5466cf, 0x34e90c6c,
  0xc0ac29b7, 0xc97c50dd, 0x3f84d5b5, 0xb5470917,
  0x9216d5d9, 0x8979fb1b,
};
const PROGMEM DWORD bf_S[4][256] = {
```

That's about it. The rest of the code will work unchanged on (tested with boards I own):

* ESP32
* Arduino Uno
* Arduino Mega
* BastWAN / RAK4260 (ATSAMR34J18B)