---
description: "TextFile is deprecated. Use IndexedFile instead. The TextFile function returns a string containing the name of the indexth TEXT file from the folder specified…"
slug: /commands/textfile
---

<div className="command-signature">

## <strong>TextFile</strong> (<em>pathName</em>, <em>index</em>  [, <em>creatorStr</em> ]) {#textfile}

</div>

:::warning
TextFile is deprecated. Use [IndexedFile](/igorpro/commands/indexedfile.md) instead.
:::

The TextFile function returns a string containing the name of the *index*th TEXT file from the folder specified by *pathName*.

Igor considers files with ".txt" extensions to be of type TEXT.

### *Details* {#details}
TextFile returns an empty string ("") if there is no such file.

*pathName* is the name of an Igor symbolic path; it is *not* a string.

*index* starts from zero.

*creatorStr* is no longer supported. This argument is ignored on Windows systems.

The order of files in a folder is determined by the operating system.

### *Examples* {#examples}
You can use TextFile in a procedure to sequence through each TEXT file in a folder, put the name of the text file into a string variable, and use this string variable as a parameter to the [LoadWave](/igorpro/commands/loadwave.md) or [Open](/igorpro/commands/open.md) operations:


```igor
Function/S PrintFirstLineOfTextFiles(pathName)
	String pathName                 // Name of an Igor symbolic path.

	Variable refNum, index
	String str, fileName
	index = 0
	do
		fileName = TextFile($pathName, index)
		if (strlen(fileName) == 0)
			break                     // No more files
		endif
		Open/R/P=$pathName refNum as fileName
		FReadLine refNum, str       // Read first line including CR/LF
		Print fileName +":" + str   // Print file name and first line
		Close refNum
		index += 1                  // Next file
	while (1)
End
```

### *See Also* {#see-also}
[IndexedFile](/igorpro/commands/indexedfile.md), [IndexedDir](/igorpro/commands/indexeddir.md), [Open](/igorpro/commands/open.md), [LoadWave](/igorpro/commands/loadwave.md)