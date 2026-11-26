---
description: "The MoveWave operation removes the source wave and places it in the specified location optionally with a new name."
slug: /commands/movewave
---

<div className="command-signature">

## <strong>MoveWave</strong>  <em>sourceWave</em>, [<em>destDataFolderPath</em>:] [<em>newName</em> ] {#movewave}

</div>

The MoveWave operation removes the source wave and places it in the specified location optionally with a new name.

If you want to rename a wave without moving it, use [Rename](/igorpro/commands/rename.md) instead.

### *Parameters* {#parameters}
*sourceWave* can be just the name of a wave in the current data folder, a partial path (relative to the current data folder) and wave name, an absolute path (starting from root) and wave name, or a wave reference variable in a user-defined function.

*destDataFolderPath* can be a partial path (relative to the current data folder), an absolute path (starting from root), or a data folder reference (DFREF) in a user-defined function.  If the destination is a null DFREF, the wave is moved to the current data folder.

### *Details* {#details}
An error is issued if a variable or wave of the same name already exists at the destination.

### *MoveWave Destination* {#movewave-destination}
Depending on the syntax you use, MoveWave may move *sourceWave* to another data folder, rename *sourceWave*, or both. To explain this, we show examples below which call this setup function:


```igor
Function Setup()
	SetDataFolder root:
	KillDataFolder root:	// clear out any previous stuff
	NewDataFolder/O root:DF0
	Make/O root:wave0
End
```

The Setup function gives you a data hierarchy like this:


```igor
root (<- current data folder)
	wave0
	DF0

// 1. Simple dest name: Renames wave0 as wave1
Function Demo1()
	Setup()
	Wave w = root:wave0
	MoveWave w, wave1	// Use Rename instead
End

// 2. Dest path with trailing colon: Moves wave0 without renaming
Function Demo2()
	Setup()
	Wave w = root:wave0
	MoveWave w, root:DF0:
End

// 3. Dest path with trailing colon and name: Moves wave0 and renames as wave1
Function Demo3()
	Setup()
	Wave w = root:wave0
	MoveWave w, root:DF0:wave1
End

// 4. DFREF dest without trailing colon: Moves wave0 without renaming
Function Demo4()
	Setup()
	Wave w = root:wave0
	DFREF dfr = root:DF0
	MoveWave w, dfr
End

// 5. DFREF dest with trailing colon: Generates error
Function Demo5()
	Setup()
	Wave w = root:wave0
	DFREF dfr = root:DF0
	MoveWave w, dfr:	// Error - trailing colon not allowed
End

// 6. Dest path with trailing colon and name: Moves wave0 and renames as wave1
Function Demo6()
	Setup()
	Wave w = root:wave0
	DFREF dfr = root:DF0
	MoveWave w, dfr:wave1
End

// 7. Null DFREF as destination; moves to current data folder
Function Demo7()
	Setup()
	Wave w = root:wave0
	SetDataFolder root:DF0	// make DF0 the current data folder
	DFREF noDF = $"Doesnotexist"
	MoveWave w, noDF	// moves to current DF
end

// 8. Use MoveWave to make a wave free (move it to no data folder)
Function Demo8()
	Setup()
	Wave w = root:wave0
	// Doesn't do it:
	//DFREF noDF = $"Doesnotexist"
	//MoveWave w, noDF	// moves to current DF
	DFREF freedf = NewFreeDataFolder()
	MoveWave w, freedf
	KillDataFolder freedf
	// as long as wave reference w remains,
	// the wave will continue to exist, and is a free wave
end
```

### *See Also* {#see-also}
[MoveString](/igorpro/commands/movestring.md), [MoveVariable](/igorpro/commands/movevariable.md), [Rename](/igorpro/commands/rename.md), [Data Folders](/igorpro/igor-basics/data-folders.md)