---
layout: cheatsheet
tags: encode
section:
  - name: Encode
    commands:
      Generate from string: qrencode [--8bit] [--level H] --output qr.png "This is my text"
  - name: Decode
    commands:
      Decode from .png file: zbarimg -1 --raw -q -Sbinary qr.png
      Decode from camera: zbarcam -1 --raw -Sbinary
---

There are four modes to encode data:

| **Number** | **Mode**                              | **First 4 bits** | **Allowed characters**                    |
|------------|---------------------------------------|------------------|-------------------------------------------|
| 1          | Numeric                               | 1 = 0b0001       | [0-9]                                     |
| 2          | Alphanumeric (only uppercase letters) | 2 = 0b0010       | [0-9][A-Z], space, $, %, *, +, -, ., /, : |
| 3          | Byte encoding (8 bits)                | 4 = 0b0100       | ISO/IEC 8859-1                            |
| 4          | Kanji                                 | 8 = 0b1000       | Shift JIS X 0208                          |

qrencode will automatically decide which mode fits best.
There is no way to specify numeric mode and fail if invalid letters are part of the encoded message.
The only way to enforce a mode is to explicitly set *--8bit*.

There are four levels of error correction:

| **Error Correction Level** | **Redundancy** | **error_correction_level number** |
|----------------------------|----------------|-----------------------------------|
| Level L (Low)              | 7%             | 1                                 |
| Level M (Medium)           | 15%            | 0                                 |
| Level Q (Quartile)         | 25%            | 3                                 |
| Level H (High)             | 30%            | 2                                 |
