---
description: "The FBinWrite operation writes the named object in binary to a file. refNum is a file reference number from the Open operation used to open the file."
slug: /commands/fbinwrite
---

<div className="command-signature">

## <strong>FBinWrite</strong>  [/B[=<em>b</em> ]/F=<em>f</em> ] <em>refNum</em>, <em>objectName</em> {#fbinwrite}

</div>

The FBinWrite operation writes the named object in binary to a file.

### *Parameters* {#parameters}
*refNum* is a file reference number from the Open operation used to open the file.

*objectName* is the name of a numeric variable, string variable, structure, or wave.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B[ = *b* ]</span> | Specifes file byte ordering. |
|  |<table class="nested-table"><tbody><tr><td>*b*&nbsp;=0:</td><td>Native (same as no /B).</td></tr><tr><td>*b*&nbsp;=1:</td><td>Reversed (same as /B).</td></tr><tr><td>*b*&nbsp;=2:</td><td>Big-endian (Motorola).</td></tr><tr><td>*b*&nbsp;=3:</td><td>Little-endian (Intel).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/F = *f*</span> | Controls the number of bytes written and how the bytes are formatted when written. |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>Native binary format of the object (default).</td></tr><tr><td>*f*&nbsp;=1:</td><td>Signed byte; one byte.</td></tr><tr><td>*f*&nbsp;=2:</td><td>Signed 16-bit word; two bytes.</td></tr><tr><td>*f*&nbsp;=3:</td><td>Signed 32-bit word; four bytes.</td></tr><tr><td>*f*&nbsp;=4:</td><td>32-bit IEEE floating point; four bytes.</td></tr><tr><td>*f*&nbsp;=5:</td><td>64-bit IEEE floating point; eight bytes.</td></tr><tr><td>*f*&nbsp;=6:</td><td>64-bit integer; eight bytes. Requires Igor Pro 7.00 or later.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/P</span> | Adds an IgorBinPacket to the data. This was used for PPC result packets (*refNum* = 0) and is not normally of use when writing to a file. |
| <span class="table-cell-nowrap">/U</span> | Integer formats (/F=1, 2, or 3) are unsigned. If /U is omitted, integers are signed. |

### *Details* {#details}
A zero value of *refNum* is used in conjunction with Program-to-Program Communication (PPC) [ActiveX Automation](/igorpro/advanced-topics.md#activex-automation) (Windows). The data that would normally be written to a file is appended to the PPC or ActiveX Automation result packet.

If the object is a string variable then /F doesn't apply. The number of bytes written is the number of bytes in the string.

The binary format that FBinWrite uses for numeric variables or waves depends on the /F flag. If no /F flag is present, FBinWrite uses the native binary format of the named object.

Byte ordering refers to the order in which a multibyte datum is written to a file. For example, a 16-bit word (sometimes called a "short") consists of a high-order byte and a low-order byte. Under big-endian byte ordering the high-order byte is written to the file first. Under little-endian byte ordering the low-order byte is written to the file first.

FBinWrite will write an entire structure to a disk file. The individual fields of the structure will be byte-swapped if the /B flag is designated.

The FBinWrite operation is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

### *See Also* {#see-also}
[FBinRead](/igorpro/commands/fbinread.md), [Open](/igorpro/commands/open.md), [FGetPos](/igorpro/commands/fgetpos.md), [FSetPos](/igorpro/commands/fsetpos.md), [FStatus](/igorpro/commands/fstatus.md), [GBLoadWave](/igorpro/commands/gbloadwave.md)