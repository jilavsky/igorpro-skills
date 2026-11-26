---
description: "The WaveCRC function returns a 32-bit cyclic redundancy check value of the bytes in the named wave starting with inCRC."
slug: /commands/wavecrc
---

<div className="command-signature">

## <strong>WaveCRC</strong> (<em>inCRC</em>, <em>waveName</em> [,<em>checkHeader</em>]) {#wavecrc}

</div>

The WaveCRC function returns a 32-bit cyclic redundancy check value of the bytes in the named wave starting with *inCRC*.

Pass 0 for *inCRC* the first time you call WaveCRC for a particular stream of bytes as represented by the wave data.

Pass the last-returned value from WaveCRC for *inCRC* if you are creating a CRC value for a given stream of bytes through multiple calls to WaveCRC.

*waveName* may be a numeric or text wave.

*checkHeader* is optional. If present, its value determines how much of the wave is checked:

| checkHeader | What It Does |
| --- | --- |
| 0 | Check only the wave data (default). |
| 1 | Check only the internal binary header. |
| 2 | Check both. |

### *Details* {#details}
Polynomial used is:


x<sup>32</sup> + x<sup>26</sup> + x<sup>23</sup> + x<sup>22</sup> + x<sup>16</sup> + x<sup>12</sup> + x<sup>11</sup> + x<sup>10</sup> + x<sup>8</sup> + x<sup>7</sup> + x<sup>5</sup> + x<sup>4</sup> + x<sup>2</sup> + x + 1

See crc32.c in the public domain source code for zlib for more information.

### *See Also* {#see-also}
[StringCRC](/igorpro/commands/stringcrc.md), [Hash](/igorpro/commands/hash.md), [WaveHash](/igorpro/commands/wavehash.md), [WaveModCount](/igorpro/commands/wavemodcount.md)