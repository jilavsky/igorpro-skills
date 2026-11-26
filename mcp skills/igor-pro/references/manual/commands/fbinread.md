---
description: "The FBinRead operation reads binary data from the file specified by refNum into the named object."
slug: /commands/fbinread
---

<div className="command-signature">

## <strong>FBinRead</strong>  [/B[=<em>b</em> ]/F=<em>f</em> ] <em>refNum</em>, <em>objectName</em> {#fbinread}

</div>

The FBinRead operation reads binary data from the file specified by *refNum*  into the named object.

For simple applications of loading binary data into numeric waves you may find the [GBLoadWave](/igorpro/commands/gbloadwave.md) operation simpler to implement.

### *Parameters* {#parameters}
*refNum* is a file reference number from the Open operation used to open the file.

*objectName* is the name of a numeric variable, string variable, structure, or wave.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B[ = *b* ]</span> | Specifes file byte ordering. |
|  |<table class="nested-table"><tbody><tr><td>*b*&nbsp;=0:</td><td>Native (same as no /B).</td></tr><tr><td>*b*&nbsp;=1:</td><td>Reversed (same as /B).</td></tr><tr><td>*b*&nbsp;=2:</td><td>Big-endian (Motorola).</td></tr><tr><td>*b*&nbsp;=3:</td><td>Little-endian (Intel).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/F = *f*</span> | Controls the number of bytes read and how the bytes are interpreted. |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>Native binary format of the object (default).</td></tr><tr><td>*f*&nbsp;=1:</td><td>Signed one-byte integer.</td></tr><tr><td>*f*&nbsp;=2:</td><td>Signed 16-bit word; two bytes.</td></tr><tr><td>*f*&nbsp;=3:</td><td>Signed 32-bit word; four bytes.</td></tr><tr><td>*f*&nbsp;=4:</td><td>32-bit IEEE floating point; four bytes.</td></tr><tr><td>*f*&nbsp;=5:</td><td>64-bit IEEE floating point; eight bytes.</td></tr><tr><td>*f*&nbsp;=6:</td><td>64-bit integer; eight bytes. Requires Igor Pro 7.00 or later.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/U</span> | Integer formats (/F=1, 2, 3, or 6) are unsigned. If /U is omitted, integers are signed. |

### *Details* {#details}
If *objectName* is the name of a string variable then /F does not apply. The number of bytes read is the number of bytes in the string before the FBinRead operation is called. You can use the [PadString](/igorpro/commands/padstring.md) function to set the size of a string.

The binary format that FBinRead uses for a numeric variable depends on the /F flag. If you omit /F, the native data type of the variable, which is 8-byte double-precision floating point, is used. So, when reading into a real numeric variable, depending on /F, FBinRead reads 1, 2, 4, or 8 bytes from the file, converts those bytes to double-precision floating point if necessary, and stores the resulting value in the variable. When reading into a complex numeric variable, this process is repeated twice, once for the real part and once for the imaginary part.

Reading real waves works like reading real variables except that a real wave has multiple elements each of which is 1, 2, 4, or 8 bytes depending on the wave's data type. For each element of a real wave, FBinRead reads the number of bytes implied by /F or by the wave's native data type, converts those bytes to the wave's data type if necessary, and stores the resulting value in the corresponding wave element. When reading into a complex wave, this process is repeated twice, once for the real part of each element and once for the imaginary part.

Reading structures is different. The /F flag has no effect. FBinReads reads the number of bytes required to fill the structure which depends on the sizes of the individual fields and the fact that Igor uses 2-byte structure alignment. After the bytes are read from the file into the structure, FBinRead byte-swaps the individual fields if you include the /B flag.

The FBinRead operation is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

### *See Also* {#see-also}
[FBinWrite](/igorpro/commands/fbinwrite.md), [Open](/igorpro/commands/open.md), [FGetPos](/igorpro/commands/fgetpos.md), [FSetPos](/igorpro/commands/fsetpos.md), [FStatus](/igorpro/commands/fstatus.md), [GBLoadWave](/igorpro/commands/gbloadwave.md)