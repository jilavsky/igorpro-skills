---
description: "The IndexedDir function returns a string containing the name of or the full path to the index'th folder in the folder referenced by pathName."
slug: /commands/indexeddir
---

<div className="command-signature">

## <strong>IndexedDir</strong> (<em>pathName</em>, <em>index</em>, <em>flags</em> [, <em>separatorStr</em>]) {#indexeddir}

</div>

The IndexedDir function returns a string containing the name of or the full path to the *index*'th folder in the folder referenced by *pathName*.

Returns a null string if the Igor symbolic path cannot be found. You can test for a null string using [strlen](/igorpro/commands/strlen.md) which returns NaN if the string is null.

Returns an empty string ("") if the index number is larger than the number of directories under the Igor symbolic path; or if the Igor symbolic path does not contain any child directories.

### *Parameters* {#parameters}
*pathName* is the name of an Igor symbolic path pointing to the parent directory.

*index* is the index number of the directory (within the parent directory) of interest starting from 0. If index is -1, IndexedDir will return the name of *all* of the folders in the parent, separated by semicolons or by *separatorStr* if specified.

*flags* is a bitwise parameter:

|  |  |
| --- | --- |
| Bit 0: | Set if you want a full path. Cleared if you want just the directory name. |

All other bits are reserved and should be cleared.


See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.

*separatorStr* is an optional string argument used when index is -1. If you omit *separatorStr*, folder names are separated by semicolons. This parameter was added in Igor 9.01.

### *Details* {#details}
You create the symbolic path identifying the parent directory using the [NewPath](/igorpro/commands/newpath.md) operation or the New Path dialog (Misc menu).

Prior to Igor Pro 3.1, IndexedDir was an external function and took a string as the first parameter rather than a name. The *pathName* parameter can now be either a name or a string containing a name. Any of the following will work:


```igor
String str = "IGOR"
Print IndexedDir(IGOR, 0, 0)    // First parameter is a name.
Print IndexedDir($str, 0, 0)    // First parameter is a name.
Print IndexedDir("IGOR", 0, 0)  // First parameter is a string.
Print IndexedDir(str, 0, 0)     // First parameter is a string.
```

The acceptance of a string is for backward compatibility only. New code should be written using a name.

The returned path uses the native conventions of the OS under which Igor is running.

### *Example: Recursively Listing Directories and Files* {#example-recursively-listing-directories-and-files}
Here is an example for heavy-duty Igor Pro programmers. It is an Igor Pro user-defined function that prints the paths of all of the files and folders in a given folder with or without recursion. You can rework this to do something with each file instead of just printing its path.

To try the function, copy and paste it into the Procedure window. Then execute the example shown in the comments.


```igor
//	PrintFoldersAndFiles(pathName, extension, recurse, level)
//	Shows how to recursively find all files in a folder and subfolders.
//	pathName is the name of an Igor symbolic path that you created
//	using NewPath or the Misc->New Path menu item.
//	extension is a file name extension like ".txt" or "????" for all files.
//	recurse is 1 to recurse or 0 to list just the top-level folder.
//	level is the recursion level - pass 0 when calling PrintFoldersAndFiles.
//	Example: PrintFoldersAndFiles("Igor", ".ihf", 1, 0)
Function PrintFoldersAndFiles(pathName, extension, recurse, level)
	String pathName     // Name of symbolic path in which to look for folders and files.
	String extension    // File name extension (e.g., ".txt") or "????" for all files.
	Variable recurse    // True to recurse (do it for subfolders too).
	Variable level      // Recursion level. Pass 0 for the top level.
	
	Variable folderIndex, fileIndex
	String prefix
	
	// Build a prefix (a number of tabs to indicate the folder level by indentation)
	prefix = ""
	folderIndex = 0
	do
		if (folderIndex >= level)
			break
		endif
		prefix += "\t"  // Indent one more tab
		folderIndex += 1
	while(1)
	
	// Print folder
	String path
	PathInfo $pathName  // Sets S_path
	path = S_path
	Printf "%s%s\r", prefix, path

	// Print files
	fileIndex = 0
	do
		String fileName
		fileName = IndexedFile($pathName, fileIndex, extension)
		if (strlen(fileName) == 0)
			break
		endif
		Printf "%s\t%s%s\r", prefix, path, fileName
		fileIndex += 1
	while(1)
	
	if (recurse)        // Do we want to go into subfolder?
		folderIndex = 0
		do
			path = IndexedDir($pathName, folderIndex, 1)
			if (strlen(path) == 0)
				break   // No more folders
			endif

			String subFolderPathName = "tempPrintFoldersPath_" + num2istr(level+1)
			
			// Now we get the path to the new parent folder
			String subFolderPath
			subFolderPath = path
			
			NewPath/Q/O $subFolderPathName, subFolderPath
			PrintFoldersAndFiles(subFolderPathName, extension, recurse, level+1)
			KillPath/Z $subFolderPathName
			
			folderIndex += 1
		while(1)
	endif
End
```

### *Example: Fast Scan of Directories* {#example-fast-scan-of-directories}
Calling IndexedDir for each directory is an O(N<sup>2</sup>) problem because to get the nth directory the OS routines underlying IndexedDir need to iterate through directories 0..n-1. This becomes an issue only if you are dealing with hundreds or thousands of directories.

This function illustrates a technique for converting this to an O(N) problem by getting a complete list of paths from IndexedDir in one call and storing them in a text wave. This approach could also be used with IndexedFile


```igor
Function ScanDirectories(pathName, printDirNames)
	String pathName         // Name of Igor symbolic path
	Variable printDirNames  // True if you want to print the directory names

	Variable t0 = StopMSTimer(-2)

	String dirList = IndexedDir($pathName, -1, 0)
	Variable numDirs = ItemsInList(dirList)

	// Store directory list in a free text wave.
	// The free wave is automatically killed when the function returns.
	Make/N=(numDirs)/T/FREE dirs = StringFromList(p, dirList)

	String dirName
	Variable i
	for(i=0; i<numDirs; i+=1)
		dirName = dirs[i]
		Print i, dirName 
	endfor

	Variable t1 = StopMSTimer(-2)
	Variable elapsed = (t1 - t0) / 1E6
	Printf "Took %g seconds\r", elapsed
End
```