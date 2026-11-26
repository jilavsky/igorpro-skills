---
description: "The CreateDataObjectName function returns a name suitable for use for a new object of the type specified by objectType."
slug: /commands/createdataobjectname
---

<div className="command-signature">

## <strong>CreateDataObjectName</strong> (<em>dfr</em>, <em>nameInStr</em>, <em>objectType</em>, <em>suffixNum</em>, <em>options</em>) {#createdataobjectname}

</div>

The CreateDataObjectName function returns a name suitable for use for a new object of the type specified by *objectType*. It can replace a combination of [CleanupName](/igorpro/commands/cleanupname.md) and [UniqueName](/igorpro/commands/uniquename.md).

CreateDataObjectName was added in Igor Pro 9.00 or later.

### *Parameters* {#parameters}
*dfr* is a data folder reference for the data folder in which the objects are to be created. Pass : for the current data folder.

*nameInStr* must contain an unquoted (i.e., no single quotes for liberal names) name, such as you might receive from the user through a dialog or control panel.

*objectType* is one of the following:

|  |  |
| --- | --- |
| 1: | Wave |
| 3: | Numeric variable |
| 4: | String variable |
| 11: | Data folder |

*suffixNum* is a value used in generating a series of names from a base name when allowing overwriting. For other uses, pass 0 for suffixNum. See ***Generating a Series of Names from a Base Name*** below.

*options* is a bitwise parameter with the bits defined as follows:


|  |  |
| --- | --- |
| Bit 0: | Be liberal. |
|  | If cleared, CreateDataObjectName always returns a standard object name. If set, it returns a liberal object name if *nameInStr* is liberal. See [Object Names](/igorpro/igor-basics/using-igor.md#object-names) for a discussion of standard and liberal object names. |
|  | If *objectType* is 3 (numeric variable) or 4 (string variable), the output name will not be liberal, even if this bit is set as Igor allows only wave and data folder names to be liberal. |
| Bit 1: | Allow overwrite. |
|  | If cleared, CreateDataObjectName returns a name that is unique in the namespace of the type of object specified by *objectType*. If set, CreateDataObjectName returns a name that may be in use in that namespace. |
|  | Waves, numeric variables and string variables are in the same namespace and so must have unique names within a given data folder. Data folders are in their own namespace and so their names can be the same as the names of waves, numeric variables and string variables. |
| Bit 2: | Input name is a base name. |
|  | If cleared, *nameInStr* is taken to be a proposed object name that CreateDataObjectName cleans up (i.e., makes legal). If the name is in use and allow overwrite is not specified, CreateDataObjectName makes the name unique by appending one or more digits. |
|  | If set, *nameInStr* is taken to be a proposed base name for a series of objects and the output name always has at least one digit appended. CreateDataObjectName cleans the name up and then appends one or more digits. If allow overwrite is not specified, the appended digits are chosen to return a unique name. If allow overwrite is specified, the appended digits represent *suffixNum* whether there is an existing object with the resulting name or not. |
|  | For an example using a base name, see ***Generating a Series of Names from a Base Name*** next. |

### *Generating a Series of Names from a Base Name* {#generating-a-series-of-names-from-a-base-name}
If you are creating a series of waves, such as when loading a data file containing multiple columns, it is sometimes convenient to generate names of the form \<baseName\>\<number\>, for example, wave0, wave1, wave2. To do this, you pass the base name as the *nameInStr* parameter and set bit 2 (input name is base name) of the *options* parameter.

If you disallow creation of names that are in use for existing objects (bit 1 of *options* cleared), CreateDataObjectName appends a number to the base name such that the output name is not in use for an object in the namespace of the type of object specified by *objectType*. In this case, *suffixNum* is not used and you should pass 0 for it.

If you allow creation of names that are in use for existing objects (bit 1 of *options* set), CreateDataObjectName appends the digits representing *suffixNum* to the base name to create the output name. In this case, you must pass the desired suffix number in each call to CreateDataObjectName.

Here is an example demonstrating this technique:


```igor
Function/S CreateSeriesOfWavesWithBaseName(dfr, baseName, beLiberal, allowOverwrite, numWavesToCreate)
	DFREF dfr           // : for current data folder
	String baseName
	int beLiberal
	int allowOverwrite
	int numWavesToCreate
	
	int options = 4     // inNameIsBaseName
	if (beLiberal)
		options += 1
	endif
	if (allowOverwrite)
		options += 2
	endif
	
	int suffixNum = 0
	String list = ""

	int i
	for(i=0; i<numWavesToCreate; i+=1)
		String outName = CreateDataObjectName(dfr, baseName, 1, suffixNum, options)
		Make/O/N=(100) dfr:$outName
		list += outName + ";"
		if (allowOverwrite)
			suffixNum += 1	// suffixNum for next call
		endif
	endfor

	return list
End
```

With overwrite disallowed, you must create the object each time through the loop because that is the only way that CreateDataObjectName can determine that the wave created in a previous iteration exists.

With overwrite allowed, you do not need to create the object each time through the loop although that is normally what you want.

### *See Also* {#see-also}
[Object Names](/igorpro/igor-basics/using-igor.md#object-names), [Programming With Liberal Names](/igorpro/programming/programming-techniques.md#programming-with-liberal-names), [CheckName](/igorpro/commands/checkname.md), [CleanupName](/igorpro/commands/cleanupname.md), [UniqueName](/igorpro/commands/uniquename.md)