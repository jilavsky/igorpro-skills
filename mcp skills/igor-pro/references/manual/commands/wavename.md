---
description: "The WaveName function returns a string containing the name of the indexth wave of the specified type in the named window or subwindow."
slug: /commands/wavename
---

<div className="command-signature">

## <strong>WaveName</strong> (<em>windowNameStr</em>, <em>index</em>, <em>type</em>) {#wavename}

</div>

The WaveName function returns a string containing the name of the *index*th wave of the specified *type* in the named window or subwindow.

### *Parameters* {#parameters}
*windowNameStr* can be "" to refer to the top graph or table.

When identifying a subwindow with *windowNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

### *Details* {#details}
WaveName works on waves displayed in a graph, in a table or on the list of waves in the current data folder. If the window is a table, WaveName returns the column name (e.g., "wave0.d"), rather than the name of the wave itself (e.g., "wave0").

For most uses, we recommend that you use [WaveRefIndexed](/igorpro/commands/waverefindexed.md) or [WaveRefIndexedDFR](/igorpro/commands/waverefindexeddfr.md) instead of WaveName. WaveName returns a string containing the wave name only, with no data folder path qualifying it. Thus, you may get erroneous results if the wave referred to in the graph has the same name as a different wave in the current data folder. Likewise, if the named wave resides in a data folder that is not the current data folder, you will not be able to refer to the named wave. Use [WaveRefIndexedDFR](/igorpro/commands/waverefindexeddfr.md) instead.

*windowNameStr* is a string expression containing the name of a graph or table or an empty string (""). If *windowNameStr* is empty and *type* is 4 then WaveName works on the list of all waves in the current data folder. If the string is empty and the type parameter is not 4 then WaveName works on the top graph or table.

*index* starts from zero.

*type* is a number from 1 to 4. When *type* is 4 and *windowNameStr* is "", WaveName works on the list of all waves in the current data folder.

For graph windows, *type* is 1 for y waves, 2 for x waves, 3 for either y or x waves.

For table windows, *type* is 1 for data columns, 2 for index or dimension label columns, 3 for either data or index or dimension label columns.

WaveName returns an empty string ("") if there is no wave matching the parameters.

### *Examples* {#examples}

```igor
WaveName("",0,4)        // Returns name first wave current data folder.
WaveName("",0,1)        // Returns name of first Y wave in top graph.
WaveName("Graph0",1,2)  // Returns name of second X wave in Graph0.
WaveName("Table0",1,3)  // Returns name of second column in Table0.
```