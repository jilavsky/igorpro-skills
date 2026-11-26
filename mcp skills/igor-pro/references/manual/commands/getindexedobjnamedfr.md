---
description: "The GetIndexedObjNameDFR function returns a string containing the name of the indexth object of the specified type in data folder referenced by dfr."
slug: /commands/getindexedobjnamedfr
---

<div className="command-signature">

## <strong>GetIndexedObjNameDFR</strong> (<em>dfr</em>, <em>objectType</em>, <em>index</em> ) {#getindexedobjnamedfr}

</div>

The GetIndexedObjNameDFR function returns a string containing the name of the *index*th object of the specified type in data folder referenced by *dfr*.

GetIndexedObjNameDFR is the same as GetIndexedObjName except the first parameter,*dfr*, is a data folder reference instead of a string containing a path.

### *Parameters* {#parameters}
*index* starts from zero. If no such object exists a zero length string ("") is returned.

*objectType* is one of the following values:

|  |  |
| --- | --- |
| 1: | Waves |
| 2: | Numeric variables |
| 3: | String variables |
| 4: | Data folders |

### *Examples* {#examples}

```igor
Function PrintAllWaveNames()
	String objName
	Variable index = 0
	DFREF dfr = GetDataFolderDFR()	// Reference to current data folder
	do
		objName = GetIndexedObjNameDFR(dfr, 1, index)
		if (strlen(objName) == 0)
			break
		endif
		Print objName
		index += 1
	while(1)
End
```

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md), [Data Folder References](/igorpro/programming/programming.md#data-folder-references), [Built-in DFREF Functions](/igorpro/programming/programming.md#built-in-dfref-functions), [CountObjectsDFR](/igorpro/commands/countobjectsdfr.md)