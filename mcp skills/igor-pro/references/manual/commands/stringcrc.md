---
description: "The StringCRC function returns a 32-bit cyclic redundancy check value of bytes in str starting with inCRC."
slug: /commands/stringcrc
---

<div className="command-signature">

## <strong>StringCRC</strong> (<em>inCRC</em>, <em>str</em>) {#stringcrc}

</div>

The StringCRC function returns a 32-bit cyclic redundancy check value of bytes in *str* starting with *inCRC*.

Pass 0 for *inCRC* the first time you call StringCRC for a particular stream of bytes as represented by the string data.

Pass the last-returned value from StringCRC for *inCRC* if you are creating a CRC value for a given stream of bytes through multiple calls to StringCRC.

### *Details* {#details}
Polynomial used is:

x<sup>32</sup>+x<sup>26</sup>+x<sup>23</sup>+x<sup>22</sup>+x<sup>16</sup>+x<sup>12</sup>+x<sup>11</sup>+x<sup>10</sup>+x<sup>8</sup>+x<sup>7</sup>+x<sup>5</sup>+x<sup>4</sup>+x<sup>2</sup>+x+1

See crc32.c in the public domain source code for zlib for more information.

### *See Also* {#see-also}
[WaveCRC](/igorpro/commands/wavecrc.md), [Hash](/igorpro/commands/hash.md), [WaveHash](/igorpro/commands/wavehash.md)