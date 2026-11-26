---
description: "The WaveHash function returns a hash of the bytes of the wave's data using the specified method. All contents of the wave's header are ignored."
slug: /commands/wavehash
---

<div className="command-signature">

## <strong>WaveHash</strong> (<em>wave</em>, <em>method</em>) {#wavehash}

</div>

The WaveHash function returns a hash of the bytes of the wave's data using the specified *method*. All contents of the wave's header are ignored.

### *Parameters* {#parameters}
*wave* may reference a numeric or text wave. Other wave types are not supported.

*method* is a number indicating the hash algorithm to use:

|  |  |
| --- | --- |
| 1: | SHA-256 (SHA-2) |
| 2: | MD4 |
| 3: | MD5 |
| 4: | SHA-1 |
| 5: | SHA-224 (SHA-2) |
| 6: | SHA-384 (SHA-2) |
| 7: | SHA-512 (SHA-2) |
| 8: | SHA3-224 |
| 9: | SHA3-256 |
| 10: | SHA3-384 |
| 11: | SHA3-512 |
| 100: | xxHash (XXH32) **\*** |
| 101: | xxHash (XXH64)  **\*** |
| 102: | xxHash (XXH3-64-bit)  **\*** |
| 103: | xxHash (XXH3-128 bit)  **\*** |

**\*** This algorithm is non-cryptographic. See [Non-cryptographic hash function](https://en.wikipedia.org/wiki/Non-cryptographic_hash_function) for an explanation.

See [xxHash](https://github.com/Cyan4973/xxHash) for information on the xxHash algorithms.

Methods 8-11 and 100-103 were added in Igor Pro 10.


### *See Also* {#see-also}
[WaveModCount](/igorpro/commands/wavemodcount.md), [WaveCRC](/igorpro/commands/wavecrc.md), [StringCRC](/igorpro/commands/stringcrc.md), [Hash](/igorpro/commands/hash.md)