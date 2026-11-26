---
description: "The IndexSort operation sorts the values in each sortedWaveName wave according to the Y values of indexWaveName."
slug: /commands/indexsort
---

<div className="command-signature">

## <strong>IndexSort</strong>  [ /DIML ] <em>indexWaveName</em>, <em>sortedWaveName</em> [, <em>sortedWaveName</em> ]... {#indexsort}

</div>

The IndexSort operation sorts the values in each *sortedWaveName* wave according to the Y values of *indexWaveName*.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DIML</span> | Moves the dimension labels with the values (keeps any row dimension label with the row's value). |

### *Details* {#details}
*indexWaveName* cannot be complex. *indexWaveName* is presumed to have been the destination of a previous MakeIndex operation.

This has the effect of putting the *sortedWaveName* waves in the same order as the wave from which the index values in *indexWaveName* was made.

All of the *sortedWaveName* waves must be of equal length.

### *See Also* {#see-also}
[Sorting](/igorpro/analysis/analysis.md#sorting), [MakeIndex and IndexSort](/igorpro/analysis/analysis.md#makeindex-and-indexsort), [Sort](/igorpro/commands/sort.md), [MakeIndex](/igorpro/commands/makeindex.md)