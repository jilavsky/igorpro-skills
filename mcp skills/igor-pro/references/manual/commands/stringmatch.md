---
description: "The StringMatch function tests string for a match to matchStr. You may include asterisks in matchStr as a wildcard character."
slug: /commands/stringmatch
---

<div className="command-signature">

## <strong>StringMatch</strong> (<em>string</em>, <em>matchStr</em>) {#stringmatch}

</div>

The StringMatch function tests *string* for a match to *matchStr* . You may include asterisks in *matchStr* as a wildcard character.

StringMatch returns 1 to indicate a match, 0 for no match or NaN if it ran out of memory.

### *Details* {#details}
*matchStr* is some combination of normal characters and the asterisk wildcard character that matches anything. For example:


|  |  |
| --- | --- |
| "\*" | Matches any string. |
| "xyz" | Matches the string "xyz" only. |
| "\*xyz" | Matches strings ending with "xyz", for instance "abcxyz". |
| "xyz\*" | Matches strings beginning with xyz, for instance "xyzpqr". |
| "\*xyz\*" | Matches strings containing xyz, for instance "abcxyzpqr". |
| "abc\*xyz" | Matches strings beginning with abc and ending with xyz, for instance "abcpqrxyz". |
| If *matchStr* begins with the "!" character, a match is indicated if *string* does not match *matchStr*. For example: |  |
| "!\*xyz" | Matches strings which ***do not*** end with xyz. |

The "!" character is considered to be a normal character if it appears anywhere else.

Note that matching is case-insensitive, so "xyz" also matches "XYZ" or "Xyz".

Also note that it is impossible to match an asterisk in *string*: use [GrepString](/igorpro/commands/grepstring.md) instead.

Among other uses, the StringMatch function can be used to build your own versions of the [WaveList](/igorpro/commands/wavelist.md) function, using [NameOfWave](/igorpro/commands/nameofwave.md) and stringmatch to qualify names of waves found by [WaveRefIndexedDFR](/igorpro/commands/waverefindexeddfr.md).

### *See Also* {#see-also}
[GrepString](/igorpro/commands/grepstring.md), [CmpStr](/igorpro/commands/cmpstr.md), [strsearch](/igorpro/commands/strsearch.md), [SplitString](/igorpro/commands/splitstring.md), [sscanf](/igorpro/commands/sscanf.md), [ListMatch](/igorpro/commands/listmatch.md), [ReplaceString](/igorpro/commands/replacestring.md)