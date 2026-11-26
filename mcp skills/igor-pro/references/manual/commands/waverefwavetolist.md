---
description: "The WaveRefWaveToList function returns a semicolon-separated string list containing data folder paths."
slug: /commands/waverefwavetolist
---

<div className="command-signature">

## <strong>WaveRefWaveToList</strong> (<em>waveRefWave</em>, <em>option</em>) {#waverefwavetolist}

</div>

The WaveRefWaveToList function returns a semicolon-separated string list containing data folder paths.

Each element of the returned string list is the full or partial path to the wave referenced by the corresponding element of *waveRefWave*. Entries in *waveRefWave* that are NULL or entries that correspond to free waves result in an empty list element.

The WaveRefWaveToList function was added in Igor Pro 7.00.

### *Parameters* {#parameters}
*waveRefWave* is a wave reference wave each element of which contains a reference to an existing wave or NULL (0).

*option* determines if the returned path is a full path or a partial path relative to the current data folder:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">*option* = 0:</span> | Full path. |
| <span class="table-cell-nowrap">*option* = 1:</span> | Partial path relative to the current data folder. |

Other values of *option* are reserved for the future.

### *Example* {#example}

```igor
Function Test()
	SetDataFolder root:
	Make/O/FREE aaa
	Make/O bbb
	Make/O/WAVE/N=3 wr
	Wr[0]=aaa
 	// Wr[1] is null by initialization.
	wr[2]=bbb
	String result = WaveRefWaveToList(wr,0)
	Print result
End
// Executing Test() prints:
  ;;root:bbb;
```

The first empty string corresponds to the free wave 'aaa' and the second empty string corresponds to the null entry in the wave reference wave.

### *See Also* {#see-also}
[ListToWaveRefWave](/igorpro/commands/listtowaverefwave.md), [ListToTextWave](/igorpro/commands/listtotextwave.md), [Wave References](/igorpro/programming/programming.md#wave-references)