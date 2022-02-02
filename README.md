# RAK4631_Blowfish

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