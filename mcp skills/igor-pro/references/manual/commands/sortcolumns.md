---
description: "The SortColumns operation rearranges data in columns of the sortWaves using the data movements that would sort the values of the keyWaves if they were sorted."
slug: /commands/sortcolumns
---

<div className="command-signature">

## <strong>SortColumns</strong>  [<em>flags</em>] [<em>keyWaves</em>={<em>waveList</em> }], <em>sortWaves</em>={<em>waveList</em> } {#sortcolumns}

</div>

The SortColumns operation rearranges data in columns of the *sortWaves* using the data movements that would sort the values of the *keyWaves* if they were sorted.

The SortColumns operation was added in Igor Pro 7.00.

### *Parameters* {#parameters}
*keyWaves* is an optional list of 1 or more wave references in braces separated by commas. The first listed wave is the primary sort key, the second is the secondary sort key, and so on. The *keyWaves* list can contain a maximum of 10 waves. The key waves can be either text or real numeric waves but all key waves must be of the same type and have the same number of points. Complex waves, wave reference waves and data folder reference waves cannot be used as key waves.

*sortWaves* is a lists of one or more wave references in braces separated by commas. The *sortWaves* list can contain a maximum of 100 waves.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Alphanumeric sort. |
|  | When *keyWaves* includes text waves, or the /KNDX flag is used and the first wave in the *sortWaves* list is a text wave, the normal sorting places "wave1" and "wave10" before "wave9". Use /A to sort the number portion numerically, so that "wave9" is sorted before "wave10". /A cannot be used with the /LOC flag. |
| <span class="table-cell-nowrap">/C</span> | Case-sensitive sort. When *keyWaves* includes text waves, or the /KNDX flag is used and the first wave in the *sortWaves* list is a text wave, the sort is case-insensitive unless you use the /C flag to make it case-sensitive. |
| <span class="table-cell-nowrap">/DIML</span> | Moves the row dimension labels with the data values. Column dimension labels remain unchanged. |
| <span class="table-cell-nowrap">/KNDX = {*c0*, *c1*, ... *c9* }</span> |  |
|  | Specifies up to 10 columns of the first wave in the *sortWaves* list to use as the sort keys. This flag and the *keyWaves* keyword are mutually exclusive. If this flag is used then the first wave in the *sortWaves* list must be either a real numeric or text wave. |
| <span class="table-cell-nowrap">/LOC</span> | Locale aware sort. |
|  | When k*eyWaves* includes text waves, or the /KNDX flag is used and the first wave in the *sortWaves* list is a text wave, the text encoding of the text waves' data is taken into account and sorting is done according to the sorting conventions of the current system locale. |
|  | /LOC is ignored if the text waves' data encoding is unknown, binary, Symbol, or Dingbats. |
|  | /LOC cannot be used with the /A flag. |
|  | See Details for more information. |
| <span class="table-cell-nowrap">/R</span> | Reverses the sort, sorting from largest to smallest. |

### *Details* {#details}
Waves in the *keyWaves* list are not actually sorted unless they also appear in the *sortWaves* list.

All waves must have the same number of rows but can have different numbers of columns, layers and chunks.

*keyWaves*, or the first wave in the *sortWaves* list when /KNDX is used, must be either numeric or text waves.

When the *sortWaves* list includes 3D or 4D waves, the operation sorts all columns of all layers/chunks.

The sorting algorithm used does not maintain the relative position of rows with the same key value.

When the /LOC flag is used, the bytes stored in the text wave at each point are converted into a Unicode string using the text encoding of the text wave data. These Unicode strings are then compared using OS-specific text comparison routines based on the current locale as set in the operating system. This means that the order of sorted items may differ when the same sort is done with the same data under different operating systems or different system locales.

### *Examples* {#examples}

```igor
// Define a function that creates sample data
Function CreateSampleData()
	Make/O key1={3,1,0,2}
	Make/O/T text1={"Jack","Fred","Robin","Bob"}
	Make/O w1={{1,2,3,4},{11,12,13,14}}
End

// Create sample data and display in a table
CreateSampleData()
Edit key1,text1,w1

// Sort based on a numeric key
SortColumns keyWaves=key1,sortWaves=w1

// Revert the data
CreateSampleData()

// Sort based on text key
SortColumns keyWaves=text1,sortWaves=w1

// Revert the data
CreateSampleData()

// Sort using key index
SortColumns/kndx=0 sortWaves={text1,w1}
```

### *See Also* {#see-also}
[Sorting](/igorpro/analysis/analysis.md#sorting), [Sort](/igorpro/commands/sort.md), [Reverse](/igorpro/commands/reverse.md), [SortList](/igorpro/commands/sortlist.md)