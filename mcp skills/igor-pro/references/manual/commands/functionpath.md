---
description: "The FunctionPath function returns a path to the file containing the named function."
slug: /commands/functionpath
---

<div className="command-signature">

## <strong>FunctionPath</strong> (<em>functionNameStr</em>) {#functionpath}

</div>

The FunctionPath function returns a path to the file containing the named function. This is useful in certain specialized cases, such as if a function needs access to a lookup table of a large number of values.

The most likely use for this is to find the path to the file containing the currently running function. This is done by passing "" for *functionNameStr*, as illustrated in the example below.

The returned path uses Macintosh syntax regardless of the current platform. See [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details.

If the procedure file is a normal standalone procedure file, the returned path will be a full path to the file.

If the function resides in the built-in procedure window the returned path will be ":Procedure". If the function resides in a packed procedure file, the returned path will be ":\<packed procedure window title\>".

If FunctionPath is called when procedures are in an uncompiled state, it returns ":".

### *Parameters* {#parameters}
If *functionNameStr* is "", FunctionPath returns the path to the currently executing function or "" if no function is executing.

Otherwise FunctionPath returns the path to the named function or "" if no function by that name exists.

### *Examples* {#examples}

```igor
// Load a lookup table into memory.
// The lookup table is stored as a wave in an Igor binary wave file.

Function LoadMyLookupTable()
	String path

	path = FunctionPath("")	// Path to file containing this function.
	if (CmpStr(path[0],":") == 0)
		// This is the built-in procedure window or a packed procedure
		// file, not a standalone file. Or procedures are not compiled.
		return -1
	endif
	
	// Create path to the lookup table file.
	path = ParseFilePath(1, path, ":", 1, 0) + "MyTable.ibw"

	DFREF dfSave = GetDataFolderDFR()

	// A previously-created place to store my private data.
	SetDataFolder root:Packages:MyData

	// Load the lookup table.
	LoadWave/O path

	SetDataFolder dfSave

	return 0
End
```

### *See Also* {#see-also}
[FunctionList](/igorpro/commands/functionlist.md)