---
description: "The Hash function returns a hash of the data in inputStr. The length of the resulting hash string is fixed for each algorithm."
slug: /commands/hash
---

<div className="command-signature">

## <strong>Hash</strong> (<em>inputStr</em>, <em>method</em>) {#hash}

</div>

The Hash function returns a hash of the data in *inputStr*.

The length of the resulting hash string is fixed for each algorithm.

### *Parameters* {#parameters}
*inputStr* is a string that can contain binary or text data.

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

Prior to Igor Pro 7.00, only method 1 was supported.

Methods 8-11 and 100-103 were added in Igor Pro 10.

### *See Also* {#see-also}
[WaveHash](/igorpro/commands/wavehash.md), [StringCRC](/igorpro/commands/stringcrc.md), [WaveCRC](/igorpro/commands/wavecrc.md)