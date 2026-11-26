---
description: "The CopyFile operation copies a file on disk. srcFileStr can be a full path to the file to be copied (in which case /P is not needed), a partial path relative…"
slug: /commands/copyfile
---

<div className="command-signature">

## <strong>CopyFile</strong>  [/D /I[=<em>i</em> ]/M=<em>messageStr</em> /O/P=<em>pathName</em> /S=<em>saveMessageStr</em> /Z[=<em>z</em> ] ]  [<em>srcFileStr</em> ]  [ <em>as</em> <em>destFileOrFolderStr</em> ] {#copyfile}

</div>

The CopyFile operation copies a file on disk.

### *Parameters* {#parameters}
*srcFileStr*  can be a full path to the file to be copied (in which case /P is not needed), a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*.

If Igor cannot determine the location of the source file from *srcFileStr*  and *pathName*, it displays a dialog allowing you to specify the source file.

*destFileOrFolderStr* is interpreted as the name of (or path to) an existing folder when /D is specified, otherwise it is interpreted as the name of (or path to) a possibly existing file.

If *destFileOrFolderStr* is a partial path, it is relative to the folder associated with *pathName*.

If /D is specified, the source file is copied inside the folder using the source file's name.

If Igor cannot determine the location of the destination file from *pathName* , *srcFileStr*, and *destFileOrFolderStr*, it displays a Save File dialog allowing you to specify the destination file (and folder).

If you use a full or partial path for either *srcFileStr*  or *destFileOrFolderStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

Folder paths should not end with single [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators). See [MoveFolder](/igorpro/commands/movefolder.md)'s Details section.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D</span> | Interprets *destFileOrFolderStr*  as the name of (or path to) an existing folder (or "directory"). Without /D, *destFileOrFolderStr* is interpreted as the name of (or path to) a file. |
|  | If *destFileOrFolderStr* is not a full path to a folder, it is relative to the folder associated with *pathName*. |
| <span class="table-cell-nowrap">/I[ = *i* ]</span> | Specifies the level of interactivity with the user. |
|  |<table class="nested-table"><tbody><tr><td>*i*&nbsp;=0:</td><td>Interactive only if one or *srcFileStr* or *destFileOrFolderStr* is not specified or if the source file is missing. (Same as if /I was not specified.)</td></tr><tr><td>*i*&nbsp;=1:</td><td>Interactive even if *srcFileStr* is specified and the source file exists.</td></tr><tr><td>*i*&nbsp;=2:</td><td>Interactive even if *destFileOrFolderStr* is specified.</td></tr><tr><td>*i*&nbsp;=3:</td><td>Interactive even if *srcFileStr* is specified, the source file exists, and *destFileOrFolderStr* is specified. Same as /I only.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/M = *messageStr*</span> | Specifies the prompt message in the Open File dialog. If /S is not specified, then *messageStr* will be used for both Open File and for Save File dialogs. |
| <span class="table-cell-nowrap">/O</span> | Overwrite existing destination file, if any. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the source file, and the folder into which the file is copied. *pathName* is the name of an existing symbolic path. |
|  | Using /P means that both *srcFileStr* and *destFileOrFolderStr* must be either simple file or folder names, or paths relative to the folder specified by *pathName*. |
| <span class="table-cell-nowrap">/S = *saveMessageStr*</span> | Specifies the prompt message in the Save File dialog. |
| <span class="table-cell-nowrap">/Z[ = *z* ]</span> | Prevent procedure execution from aborting if it attempts to copy a file that does not exist. Use /Z if you want to handle this case in your procedures rather than having execution abort. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Same as no /Z at all.</td></tr><tr><td>/Z=1:</td><td>Used for copying a file only if it exists. /Z alone has the same effect as /Z=1.</td></tr><tr><td>/Z=2:</td><td>Used for copying a file if it exists and displaying a dialog if it does not exist.</td></tr></tbody></table>

### *Variables* {#variables}

|  |  |
| --- | --- |
| The CopyFile operation returns information in the following variables: |  |
| V_flag | V_flag is set to zero if the file was copied, to -1 if the user cancelled either the Open File or Save File dialogs, and to some nonzero value if an error occurred, such as the specified file does not exist. |
| S_fileName | Stores the full path to the file that was copied.  If an error occurred or if the user cancelled, it is set to an empty string. |
| S_path | Stores the full path to the file copy.  If an error occurred or if the user cancelled, it is set to an empty string. |

### *Examples* {#examples}

```igor
// Copy a file within the same folder using a new name
CopyFile/P=myPath "afile.txt" as "destFile.txt"

// Copy a file into subfolder using the original name (using /P)
CopyFile/D/P=myPath "afile.txt" as ":subfolder"
Print S_Path	// prints "Macintosh HD:folder:subfolder:afile.txt"

// Copy file into subfolder using the original name (using full paths)
CopyFile/D "Macintosh HD:folder:afile.txt" as "Server:archive"

// Copy a file from one folder to another, assigning the copy a new name.
CopyFile "Macintosh HD:folder:afile.txt" as "Server:archive:destFile.txt"

// Copy user-selected file in any folder as destFile.txt in myPath folder
// (prompt to save even if destFile.txt doesn't exist)
CopyFile/I=2/P=myPath as "destFile.txt"

// Copy user-selected file in any folder as destFile.txt in any folder
CopyFile as "destFile.txt"
```

### *See Also* {#see-also}
[Operations[Open]](/igorpro/commands/open.md), [MoveFile](/igorpro/commands/movefile.md), [DeleteFile](/igorpro/commands/deletefile.md), [CopyFolder](/igorpro/commands/copyfolder.md), [Functions[IndexedFile]](/igorpro/commands/indexedfile.md), [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths)