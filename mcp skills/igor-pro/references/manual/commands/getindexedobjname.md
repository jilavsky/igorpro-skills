---
description: "The GetIndexedObjName function returns a string containing the name of the indexth object of the specified type in the data folder specified by the string…"
slug: /commands/getindexedobjname
---

<div className="command-signature">

## <strong>GetIndexedObjName</strong> (<em>sourceFolderStr</em>, <em>objectType</em>, <em>index</em>) {#getindexedobjname}

</div>

The GetIndexedObjName function returns a string containing the name of the *index*th object of the specified type in the data folder specified by the string expression.

[GetIndexedObjNameDFR](/igorpro/commands/getindexedobjnamedfr.md) is preferred.

### *Parameters* {#parameters}
*sourceFolderStr* can be either ":" or "" to specify the current data folder. You can also use a full or partial data folder path. *index* starts from zero. If no such object exists a zero length string ("") is returned.

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
	do
		objName = GetIndexedObjName(":", 1, index)
		if (strlen(objName) == 0)
			break
		endif
		Print objName
		index += 1
	while(1)
End
```

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md), [CountObjects](/igorpro/commands/countobjects.md)