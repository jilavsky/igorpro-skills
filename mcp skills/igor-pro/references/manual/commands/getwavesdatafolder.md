---
description: "The GetWavesDataFolder function returns a string containing the name of a data folder containing the wave named by waveName."
slug: /commands/getwavesdatafolder
---

<div className="command-signature">

## <strong>GetWavesDataFolder</strong> (<em>waveName</em>, <em>kind</em>) {#getwavesdatafolder}

</div>

The GetWavesDataFolder function returns a string containing the name of a data folder containing the wave named by *waveName*. Variations on the theme are selected by *kind*.

The most common use for this is in a procedure, when you want to create a wave or a global variable in the data folder containing a wave passed as a parameter.

[GetWavesDataFolderDFR](/igorpro/commands/getwavesdatafolderdfr.md) is preferred.

### *Details* {#details}

| kind | GetWavesDataFolder Action |
| --- | --- |
| 0 | Returns only the name of the data folder containing *waveName.* |
| 1 | Returns full path of data folder containing *waveName*, without wave name. |
| 2 | Returns full path of data folder containing *waveName*, including possibly quoted wave name. |
| 3 | Returns partial path from current data folder to the data folder containing *waveName.* |
| 4 | Returns partial path including possibly quoted wave name. |

Kinds 2 and 4 are especially useful in creating command strings to be passed to Execute.

### *Examples* {#examples}

```igor
Function DuplicateWaveInDataFolder(w)
	Wave w
	DFREF dfSav = GetDataFolderDFR()
	SetDataFolder GetWavesDataFolder(w,1)
	Duplicate/O w, $(NameOfWave(w) + "_2")
	SetDataFolder dfSav
End
```

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md)