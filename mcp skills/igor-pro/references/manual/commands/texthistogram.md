---
description: "The TextHistogram operation computes the histogram of a text wave where the output bins represent the counts of occurrences of each unique string found in…"
slug: /commands/texthistogram
---

<div className="command-signature">

## <strong>TextHistogram</strong>  [ <em>flags</em> ] <em>srcTextWave</em> {#texthistogram}

</div>

The TextHistogram operation computes the histogram of a text wave where the output bins represent the counts of occurrences of each unique string found in *srcTextWave*.

The TextHistogram operation was added in Igor Pro 9.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/CI</span> | Performs case-insensitive string comparison. |
|  | If you omit /CI TextHistogram performs case-sensitive comparison unless you include /LOC. |
| <span class="table-cell-nowrap">/DN = *binsCountsWave*</span> | Specifies the numeric output wave that contains the count for each bin. If you omit /DN, the numeric output wave is created in the current data folder and named W_TextHistogram. |
| <span class="table-cell-nowrap">/DT = *binsTextWave*</span> | Specifies the text output wave that contains the strings corresponding to each bin. If you omit /DT, the text output wave is created in the current data folder and named T_TextHistogram. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all output waves as a free waves. |
|  | /FREE is permitted in user-defined functions only. If you use /FREE then all output wave parameters must be simple names, not paths or $ expressions. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for details on free waves. |
| <span class="table-cell-nowrap">/LOC</span> | Performs case-insensitive string comparison following locale-aware rules. This option results in significantly slower performance. |
| <span class="table-cell-nowrap">/SORT = *mode*</span> | Sets the order of the output bins. |
|  |<table class="nested-table"><tbody><tr><td>*mode*=1:</td><td>The output waves are ordered from the bin with the largest count to the bin with the smallest count. This is the default if you omit /SORT.</td></tr><tr><td>*mode*=2:</td><td>The output waves are ordered from the bin with the longest string to the bin with the shortest string.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Suppress errors. You can use V_Flag to detect and handle errors yourself. |

### *Details* {#details}
TextHistogram does case-sensitive string comparisons unless you specify /CI or /LOC in which case it does case-insensitive string comparisons.

TextHistogram scans *srcTextWave* and counts matching string entries. It treats text waves of all dimensions as if they were 1D waves.

The output of the operation consists of two waves: a text wave containing the text corresponding to each bin and a numeric wave containing the bin counts. You can specify the destination waves using the /DT and /DN  flags. If you omit /DT the text output wave is created in the current data folder and named T_TextHistogram. If you omit /DN the numeric output wave is created in the current data folder and named W_TextHistogram. The output waves overwrite any previously-existiing waves with the same names.

The operation creates automatic wave references for the output waves specified by /DT and /DN. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. It does not create wave references for the default output waves created if you omit /DT or /DN so you need explicit wave references.

When using case-insensitive mode the output text wave may use any one of the equivalent forms of the text represented by the bin.

### *Output Variables* {#output-variables}
TextHistogram sets the following output variable:


|  |  |
| --- | --- |
| V_flag | 0 if the operation succeeded or a non-zero error code. |

### *See Also* {#see-also}
[Histogram](/igorpro/commands/histogram.md), [FindDuplicates](/igorpro/commands/findduplicates.md), [Sort](/igorpro/commands/sort.md)