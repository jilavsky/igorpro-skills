---
description: "The MakeIndex operation sets the data values of indexWave such that they give the ordering of sortKeyWaves."
slug: /commands/makeindex
---

<div className="command-signature">

## <strong>MakeIndex</strong>  [/A/C/R] <em>sortKeyWaves</em>, <em>indexWave</em> {#makeindex}

</div>

The MakeIndex operation sets the data values of *indexWave* such that they give the ordering of *sortKeyWaves*.

For simple sorting problems, there is no need to use MakeIndex. Just use the [Sort](/igorpro/commands/sort.md) operation.

### *Parameters* {#parameters}
*sortKeyWaves* is either the name of a single wave, to use a single sort key, or the name of multiple waves in braces, to use multiple sort keys.

*indexWave* must specify an existing numeric wave.

All waves must be of the same length and must not be complex.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Alphanumeric. When *sortKeyWaves* includes text waves, the normal sorting places "wave1" and "wave10" before "wave9". Use /A to sort the number portion numerically, so that "wave9" is sorted before "wave10". |
| <span class="table-cell-nowrap">/C</span> | Case-sensitive. When *sortKeyWaves* includes text waves, the ordering is case-insensitive unless you use the /C flag which makes it case-sensitive. |
| <span class="table-cell-nowrap">/LOC</span> | Performs a locale-aware sort. |
|  | When *sortKeyWaves* includes text waves, the text encoding of the text waves' data is taken into account and sorting is done according to the sorting conventions of the current system locale. This flag is ignored if the text waves' data encoding is unknown, binary, Symbol, or Dingbats. This flag cannot be used with the /A flag. See Details for more information. |
|  | The /LOC flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/R</span> | Reverse the index so that ordering is from largest to smallest. |

### *Details* {#details}
MakeIndex is used in preparation for a subsequent IndexSort operation. If /R is used the ordering is from largest to smallest. Otherwise it is from smallest to largest.

When the /LOC flag is used, the bytes stored in the text wave at each point are converted into a Unicode string using the text encoding of the text wave data. These Unicode strings are then compared using OS-specific text comparison routines based on the current locale as set in the operating system. This means that the order of sorted items may differ when the same sort is done with the same data under different operating systems or different system locales.

When /LOC is omitted the sort is done on the raw text without regard to the waves' text encoding.

### *See Also* {#see-also}
[Sorting](/igorpro/analysis/analysis.md#sorting), [MakeIndex and IndexSort](/igorpro/analysis/analysis.md#makeindex-and-indexsort), [Sort](/igorpro/commands/sort.md), [IndexSort](/igorpro/commands/indexsort.md)