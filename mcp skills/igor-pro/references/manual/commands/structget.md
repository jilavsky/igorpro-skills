---
description: "The StructGet operation reads binary numeric data from a specified column of a wave or from a string variable and copies the data into the specified structure…"
slug: /commands/structget
---

<div className="command-signature overload">

## <strong>StructGet</strong>  [/B=<em>b</em> ] <em>structVar</em>, <em>waveStruct</em> [[<em>colNum</em> ]] {#structget}

</div>
<div className="command-signature">

## <strong>StructGet</strong>  /S [/B=<em>b</em> ] <em>structVar</em>, <em>strStruct</em> {#structget}

</div>

The StructGet operation reads binary numeric data from a specified column of a wave or from a string variable and copies the data into the specified structure variable. The source wave or string will have been filled beforehand by [StructPut](/igorpro/commands/structput.md).

### *Parameters* {#parameters}
*structVar* is the name of an existing structure that will be filled with new data values.

*waveStruct* is the name of a wave containing binary numeric data that will be used to fill the structure. Use the optional *colNum* parameter to specify a column from the structure wave. The contents of *waveStruct* are created beforehand using StructPut.

*strStruct* is the name of a string variable containing binary numeric data. The contents of *strStruct* are created beforehand using StructPut.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B = *b*</span> | Sets the byte ordering for reading of structure data. |
|  |<table class="nested-table"><tbody><tr><td>*b*&nbsp;=0:</td><td>Reads in native byte order.</td></tr><tr><td>*b*&nbsp;=1:</td><td>Reads bytes in reversed order.</td></tr><tr><td>*b*&nbsp;=2:</td><td>Default; reads data in big-endian, high-byte-first order (Motorola).</td></tr><tr><td>*b*&nbsp;=3:</td><td>Reads data in little-endian, low-byte-first order (Intel).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/S</span> | Reads binary data from a string variable, which was set previously using StructPut. |

### *Details* {#details}
The data that are stored in *waveStruct* and *strStruct* are in binary format so you cannot directly view a meaningful representation of their contents by printing them or viewing the wave in a table. To view the contents of *waveStruct* or *strStruct* you must use StructGet to export them back into a structure and then retrieve the members.

If *colNum* is out of bounds it will be clipped to valid values and an error reported. If the row dimension does not match the structure size, as much data as possible will be copied to the structure.

By default, data are read in big-endian, high-byte order (Motorola). This allows data written on one platform to be read on the other.

### *See Also* {#see-also}
The [StructPut](/igorpro/commands/structput.md) operation for writing structure data to waves or strings.