---
description: "The StructPut operation copies the binary numeric data in a structure variable to a specified column in a wave or to a string variable."
slug: /commands/structput
---

<div className="command-signature overload">

## <strong>StructPut</strong>  [/B=<em>b</em> ] <em>structVar</em>, <em>waveStruct</em> [[<em>colNum</em> ]] {#structput}

</div>
<div className="command-signature">

## <strong>StructPut</strong>  /S [/B=<em>b</em> ] <em>structVar</em>, <em>strStruct</em> {#structput}

</div>

The StructPut operation copies the binary numeric data in a structure variable to a specified column in a wave or to a string variable. The data in the wave or string can be read out into another structure using [StructGet](/igorpro/commands/structget.md).

### *Parameters* {#parameters}
*structVar* is the name of a structure from which data is to be exported.

*waveStruct* is the name of an existing wave to which data will be exported. Use the optional *colNum* parameter to specify a column to contain the data. The first column of *waveStruct* will be filled if *colNum* is omitted.

*strStruct* is the name of an existing string variable to which data will be exported.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B = *b*</span> | Sets the byte ordering for writing of structure data. |
|  |<table class="nested-table"><tbody><tr><td>*b*&nbsp;=0:</td><td>Writes in native byte order.</td></tr><tr><td>*b*&nbsp;=1:</td><td>Writes bytes in reversed order.</td></tr><tr><td>*b*&nbsp;=2:</td><td>Default; writes data in big-endian, high-byte-first order (Motorola).</td></tr><tr><td>*b*&nbsp;=3:</td><td>Writes data in little-endian, low-byte-first order (Intel).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/S</span> | Writes binary data to a string variable. |

### *Details* {#details}
The structure fields to be exported must contain only numeric data in either integer, floating point, or double precision format. If the structure contains any objects such as String, NVAR, WAVE, etc., then only the numeric data at the end of the structure is copied. If there is no suitable data at the end, an error is generated at compile time. Prior to Igor Pro 8, the presence of any illegal field would result in an error.

If needed, StructPut will redimension *waveStruct* to unsigned byte format, will set the number of rows to equal the size of the structure, and set the column dimension large enough to accommodate the size specified by *colNum*. You can think of *waveStruct* as a one-dimensional array of structure contents indexed by *colNum* although the wave is actually two-dimensional with each column containing a copy of a separate structure.

By default, data are written in big-endian, high-byte order (Motorola). This allows data written on one platform to be read on the other.

### *See Also* {#see-also}
The [StructGet](/igorpro/commands/structget.md) operation for reading structure data from waves or strings.