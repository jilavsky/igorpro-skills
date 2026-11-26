---
description: "The Redimension operation remakes the named waves, preserving their contents as much as possible."
slug: /commands/redimension
---

<div className="command-signature">

## <strong>Redimension</strong>  [/B/C/D/E=<em>e</em> /I/N=<em>n</em> /R/S/U/W/Y=<em>numType</em> ] <em>waveName</em>, [<em>waveName</em> ]... {#redimension}

</div>

The Redimension operation remakes the named waves, preserving their contents as much as possible.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B</span> | Converts waves to 8-bit signed integer or unsigned integer if /U is present. |
| <span class="table-cell-nowrap">/C</span> | Converts real waves to complex. |
| <span class="table-cell-nowrap">/D</span> | Converts waves to double precision floating point. |
| /E=*e* |<table class="nested-table"><tbody><tr><td>*e*&nbsp;=0:</td><td>No special action (default).</td></tr><tr><td>*e*&nbsp;=1:</td><td>Force reshape without converting or moving data.</td></tr><tr><td>*e*&nbsp;=2:</td><td>Perform endian swap. See [FBinRead](/igorpro/commands/fbinread.md) for a discussion of endian byte ordering.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/I</span> | Converts waves to 32-bit signed integer or unsigned integer if /U is present. |
| <span class="table-cell-nowrap">/L</span> | Converts waves to 64-bit signed integer or unsigned integer if /U is present. Requires Igor Pro 7.00 or later. |
| <span class="table-cell-nowrap">/N = *n*</span> | *n* is the new number of points each wave will have. Multidimensional waves are converted to 1 dimension. |
|  | If *n* =-1, the wave is converted to a 1-dimensional wave with the original number of rows. |
| <span class="table-cell-nowrap">/N = (*n1*, *n2*, *n3*, *n4* )</span> |  |
|  | *n1*, *n2*, *n3*, *n4* specify the number of rows, columns, layers, and chunks each wave will have. Trailing zeros can be omitted (e.g., /N=(*n1*, *n2*, 0, 0) can be abbreviated as /N=(*n1*, *n2* )). If any dimension size is to remain unchanged, pass -1 for that dimension. |
| <span class="table-cell-nowrap">/R</span> | Converts complex waves to real by discarding the imaginary part. |
| <span class="table-cell-nowrap">/S</span> | Converts waves to single precision floating point. |
| <span class="table-cell-nowrap">/U</span> | Converts integer waves to unsigned. |
| <span class="table-cell-nowrap">/W</span> | Converts waves to 16-bit signed integer or unsigned integer if /U is present. |
| <span class="table-cell-nowrap">/Y = *type*</span> | Specifies wave data type. See details below. |

### *Wave Data Types* {#wave-data-types}
As a replacement for the above number type flags you can use /Y=*numType* to set the number type as an integer code. See [WaveType](/igorpro/commands/wavetype.md) for code values. Do not use /Y in combination with other type flags. This technique cannot be used to change the number type without changing the real/complex setting.

### *Details* {#details}
The waves must already exist. New points in waves that are extended are initialized to zero.

In general, Redimension does not move data from one dimension to another. For instance, if you have a 6x6 matrix wave, and you would like it to be 3x12, the rows have been shortened and the data for the last three rows is lost.

As a special case, if converting to or from a 1D wave, Redimension will leave the data in place while changing the dimensionality of the wave. For example, you can use Redimension to convert a 36-element 1D wave into a 6x6 matrix in which the elements in the first column (column 0) are the first 6 elements of the 1D wave, the elements of the second column are the next 6, etc. When redimensioning from a 1D wave, columns are filled first, then layers, followed by chunks.

### *Examples* {#examples}
Reshaping a 1D wave having 4 elements to make a 2x2 matrix:


```igor
Make/N=4 vector=x
Redimension/N=(2,2) vector
```

### *See Also* {#see-also}
[Make](/igorpro/commands/make.md), [DeletePoints](/igorpro/commands/deletepoints.md), [InsertPoints](/igorpro/commands/insertpoints.md), [Concatenate](/igorpro/commands/concatenate.md), [SplitWave](/igorpro/commands/splitwave.md)