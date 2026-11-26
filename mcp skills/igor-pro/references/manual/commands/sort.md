---
description: "The Sort operation sorts the sortedWaveNames by rearranging their data values to put the data values of sortKeyWaves in order."
slug: /commands/sort
---

<div className="command-signature">

## <strong>Sort</strong>  [ /A /DIML /C /R ] <em>sortKeyWaves</em>, <em>sortedWaveName</em> [, <em>sortedWaveName</em> ]... {#sort}

</div>

The Sort operation sorts the *sortedWaveNames* by rearranging their data values to put the data values of *sortKeyWaves* in order.

### *Parameters* {#parameters}
*sortKeyWaves* is either the name of a single wave, to use a single sort key, or the name of multiple waves in braces, to use multiple sort keys.

All waves must be of the same length.

The *sortKeyWaves* must not be complex.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A[ = *a* ]</span> | Alphanumeric sort. When *sortKeyWaves* includes text waves, the normal sorting places "wave1" and "wave10" before "wave9". |
|  | The optional *a* parameter requires Igor Pro 7.00 or later. |
|  | Use /A or /A=1 to sort the number portion numerically, so that "wave9" is sorted before "wave10". |
|  | Use /A=2 to ignore + and - characters in the text so that "Text-09" sorts before "Text-10". |
| <span class="table-cell-nowrap">/C</span> | Case-sensitive sort. When *sortKeyWaves* includes text waves, the sort is case-insensitive unless you use the /C flag to make it case-sensitive. |
| <span class="table-cell-nowrap">/DIML</span> | Moves the dimension labels with the values (keeps any row dimension label with the row's value). |
| <span class="table-cell-nowrap">/LOC</span> | Performs a locale-aware sort. |
|  | When *sortKeyWaves* includes text waves, the text encoding of the text waves' data is taken into account and sorting is done according to the sorting conventions of the current system locale. This flag is ignored if the text waves' data encoding is unknown, binary, Symbol, or Dingbats. This flag cannot be used with the /A flag. See Details for more information. |
|  | The /LOC flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/R</span> | Reversed sort. Sort from largest to smallest. |

### *Details* {#details}
*sortKeyWaves* are not actually sorted unless they also appear in the list of destination waves.

The algorithm used does not maintain the relative position of items with the same key value.

When the /LOC flag is used, the bytes stored in the text wave at each point are converted into a Unicode string using the text encoding of the text wave data. These Unicode strings are then compared using OS-specific text comparison routines based on the current locale as set in the operating system. This means that the order of sorted items may differ when the same sort is done with the same data under different operating systems or different system locales.

When /LOC is omitted the sort is done on the raw text without regard to the waves' text encoding.

### *Examples* {#examples}

```igor
Sort/R myWave,myWave        // sorts myWave in decreasing order
Sort xWave,xWave,yWave      // sorts x wave in increasing order,
                            // corresponding yWave values follow.
Make/O/T myWave={"1st","2nd","3rd","4th"}
Make/O key1={2,1,1,1}       // places 2nd, 3rd, 4th before 1st.
Make/O key2={0,1,3,2}       // arranges 2nd, 3rd, 4th as 2nd, 4th, 3rd.
Sort {key1,key2},myWave     // sorts myWave in increasing order by key1.
                            // For equal key1 values, sorted by key2.
                            // Result is myWave={"2nd","4th","3rd","1st"}
Make/O/T tw={"w1","w10","w9","w-2.1"}
Sort/A tw,tw                // sorts tw in increasing number-aware order:
                            // Result is tw={"w-2.1","w1","w9","w10"}
```

### *See Also* {#see-also}
[Sorting](/igorpro/analysis/analysis.md#sorting)

[MakeIndex](/igorpro/commands/makeindex.md), [IndexSort](/igorpro/commands/indexsort.md), [Reverse](/igorpro/commands/reverse.md), [SortColumns](/igorpro/commands/sortcolumns.md), [SortList](/igorpro/commands/sortlist.md)

[FindDuplicates](/igorpro/commands/findduplicates.md), [TextHistogram](/igorpro/commands/texthistogram.md)