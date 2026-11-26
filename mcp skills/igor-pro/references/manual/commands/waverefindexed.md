---
description: "The WaveRefIndexed function returns a wave reference to the indexth wave of the specified type in the named window or subwindow."
slug: /commands/waverefindexed
---

<div className="command-signature">

## <strong>WaveRefIndexed</strong> (<em>windowNameStr</em>, <em>index</em>, <em>type</em>) {#waverefindexed}

</div>

The WaveRefIndexed function returns a wave reference to the *index*th wave of the specified type in the named window or subwindow.

To iterate through the waves in a data folder, use [WaveRefIndexedDFR](/igorpro/commands/waverefindexeddfr.md) instead of WaveRefIndexed.

### *Parameters* {#parameters}
*windowNameStr* can be "" to refer to the top graph or table window or the current data folder.

When identifying a subwindow with *windowNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

### *Details* {#details}
WaveRefIndexed is analogous to WaveName but works better with data folders.We recommend that you use it instead of WaveName.

*windowNameStr* is a string expression containing the name of a graph or table or an empty string (""). If the string is empty and *type* is 4 then WaveRefIndexed works on Igor's list of all waves in the current data folder. If the string is empty and the type parameter is not 4 then WaveRefIndexed works on the top graph.

*index* starts from zero.

*type* is a number from 1 to 4. When *type* is 4 and *windowNameStr* is "", WaveRefIndexed works on the list of all waves in the current data folder.

For graph windows, *type* is 1 for y waves, 2 for x waves, 3 for either y or x waves.

For table windows, *type* is 1 for data columns, 2 for index or dimension label columns, 3 for either data or index or dimension label columns.

WaveRefIndexed returns a null reference (see [WaveExists](/igorpro/commands/waveexists.md)) if there is no wave matching the parameters.

### *Examples* {#examples}

```igor
WaveRefIndexed("",0,1)          // Returns first Y wave in the top graph.
WaveRefIndexed("Graph0",1,2)    // Returns second X wave in Graph0.
WaveRefIndexed("Table0",1,3)    // Returns wave in the second column in Table0.
```

### *See Also* {#see-also}
[WaveRefIndexedDFR](/igorpro/commands/waverefindexeddfr.md), [NameOfWave](/igorpro/commands/nameofwave.md), [GetWavesDataFolder](/igorpro/commands/getwavesdatafolder.md)