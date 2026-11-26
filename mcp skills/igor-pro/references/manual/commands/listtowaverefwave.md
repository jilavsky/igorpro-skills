---
description: "The ListToWaveRefWave function returns a free wave containing a wave reference for each entry in stringList that corresponds to an existing wave."
slug: /commands/listtowaverefwave
---

<div className="command-signature">

## <strong>ListToWaveRefWave</strong> (<em>stringList</em> [, <em>options</em>]) {#listtowaverefwave}

</div>

The ListToWaveRefWave function returns a free wave containing a wave reference for each entry in *stringList* that corresponds to an existing wave.

The ListToWaveRefWave function was added in Igor Pro 7.00.

### *Parameters* {#parameters}
*stringList* is a semicolon-separated string list of waves specified using full paths or partial paths relative to the current data folder.

*options* is a bit field that is 0 by default. Set bit 0 to if you want the function to generate an error (see [GetRTError](/igorpro/commands/getrterror.md)) if any of the list elements does not specify an existing wave. Other bits are reserved for future use and must be cleared.

### *Example* {#example}

```igor
Function Test()
	NewDataFolder/O/S root:TestDF    // Create empty data folder as current DF
	Make/O aaa                       // aaa will be the first wave in list
	Make/O bbb
	String strList = WaveList("*", ";", "")
	Wave/WAVE wr = ListToWaveRefWave(strList, 0)    // Returns a free wave
	Wave w = wr[0]
	Print GetWavesDataFolder(w, 2)
	Wave w = wr[1]
	Print GetWavesDataFolder(w, 2)
End
```

### *See Also* {#see-also}
[WaveRefWaveToList](/igorpro/commands/waverefwavetolist.md), [ListToTextWave](/igorpro/commands/listtotextwave.md), [Wave References](/igorpro/programming/programming.md#wave-references)