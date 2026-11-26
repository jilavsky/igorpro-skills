---
description: "The WaveRefIndexedDFR function returns a wave reference to the indexth wave in the specified data folder."
slug: /commands/waverefindexeddfr
---

<div className="command-signature">

## <strong>WaveRefIndexedDFR</strong> (<em>dfr</em>, <em>index</em>) {#waverefindexeddfr}

</div>

The WaveRefIndexedDFR function returns a wave reference to the *index*th wave in the specified data folder.

### *Parameters* {#parameters}
*dfr* is a data folder reference.

*index* is the zero-based index of the wave you want to access.

### *Details* {#details}
WaveRefIndexedDFR returns a null reference (see [WaveExists](/igorpro/commands/waveexists.md)) if there is no wave corresponding to *index* in the specified data folder.

### *Example* {#example}

```igor
// DemoWaveRefIndexedDFR can be called like this:
//	DemoWaveRefIndexedDFR(root:, 0)                 // Work on root
//	DemoWaveRefIndexedDFR(root:SubDataFolder, 0)    // Work on root:SubDataFolder
//	DemoWaveRefIndexedDFR(:, 0)                     // Work on current data folder
Function DemoWaveRefIndexedDFR(dfr, recurse)
	DFREF dfr
	Variable recurse
	
	Variable index = 0
	do
		Wave/Z w = WaveRefIndexedDFR(dfr, index)
		if (!WaveExists(w))
			break
		endif
		String path = GetWavesDataFolder(w, 2)
		Print path
		index += 1
	while(1)
	
	if (recurse)
		Variable numChildDataFolders = CountObjectsDFR(dfr, 4)
		Variable i
		for(i=0; i<numChildDataFolders; i+=1)
			String childDFName = GetIndexedObjNameDFR(dfr, 4, i)
			DFREF childDFR = dfr:$childDFName
			DemoWaveRefIndexedDFR(childDFR, 1)
		endfor
	endif
End
```

### *See Also* {#see-also}
[WaveRefIndexed](/igorpro/commands/waverefindexed.md), [NameOfWave](/igorpro/commands/nameofwave.md), [GetWavesDataFolder](/igorpro/commands/getwavesdatafolder.md)