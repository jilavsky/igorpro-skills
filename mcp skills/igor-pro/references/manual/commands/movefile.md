---
description: "The MoveFile operation moves or renames a file on disk. A file is renamed by \"moving\" it to the same folder it is already in using a different name."
slug: /commands/movefile
---

<div className="command-signature">

## <strong>MoveFile</strong>  [/D/I[=<em>i</em> ]/M=<em>messageStr</em> /O/P=<em>pathName</em> /S=<em>saveMessageStr</em> /Z[=<em>z</em> ] ]  [<em>srcFileStr</em> ]  [ <em>as</em> <em>destFileOrFolderStr</em> ] {#movefile}

</div>

The MoveFile operation moves or renames a file on disk. A file is renamed by "moving" it to the same folder it is already in using a different name.

### *Parameters* {#parameters}
*srcFileStr* can be a full path to the file to be moved or renamed (in which case /P is not needed), a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*.

If Igor cannot determine the location of the file from *srcFileStr* and *pathName*, it displays an Open File dialog allowing you to specify the source file.

*destFileOrFolderStr* is interpreted as the name of (or path to) an existing folder when /D is specified, otherwise it is interpreted as the name of (or path to) a possibly existing file.

If *destFileOrFolderStr* is a partial path, it is relative to the folder associated with *pathName*.

If /D is specified, the source file is moved inside the folder using the source file's name.

If Igor cannot determine the location of the destination file from *pathName* , *srcFileStr*, and *destFileOrFolderStr*, it displays a Save File dialog allowing you to specify the destination file (and folder).

If you use a full or partial path for either *srcFileStr* or *destFileOrFolderStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

Folder paths should not end with single [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators). See [MoveFolder](/igorpro/commands/movefolder.md)'s Details section.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D</span> | *destFileOrFolderStr* is interpreted as the name of (or path to) an existing folder (or "directory"). Without /D, *destFileOrFolderStr* is interpreted as the name of (or path to) a file. |
|  | If *destFileOrFolderStr* is not a full path to a folder, it is relative to the folder associated with *pathName*. |
| /I [=*i* ] |<table class="nested-table"><tbody><tr><td>*i*&nbsp;=0:</td><td>Interactive only if *srcFileStr* or *destFileOrFolderStr* is not specified or if the source file is missing. (Same as if /I was not specified.)</td></tr><tr><td>*i*&nbsp;=1:</td><td>Interactive even if *srcFileStr* is specified and the source file exists.</td></tr><tr><td>*i*&nbsp;=2:</td><td>Interactive even if *destFileOrFolderStr* is specified.</td></tr><tr><td>*i*&nbsp;=3:</td><td>Interactive even if *srcFileStr* is specified and the source file exists. Same as /I only.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/M = *messageStr*</span> |  |
|  | Specifies the prompt message in the Open File dialog.  If /S is not specified, then *messageStr* will be used for both Open File and for Save File dialogs. |
| <span class="table-cell-nowrap">/O</span> | Overwrite existing destination file, if any. Without /O, the user is asked if replacing the existing file is to be allowed. |
| <span class="table-cell-nowrap">/P = *pathName*</span> |  |
|  | Specifies the folder to look in for the source file, and the folder into which the file is copied. *pathName* is the name of an existing symbolic path. |
|  | Using /P means that both *srcFileStr* and *destFileOrFolderStr* must be either simple file or folder names, or paths relative to the folder specified by *pathName*. |
| <span class="table-cell-nowrap">/S = *saveMessageStr*</span> |  |
|  | Specifies the prompt message in the Save File dialog. |
| <span class="table-cell-nowrap">/Z[ = *z* ]</span> | Prevents procedure execution from aborting if it attempts to move a file that does not exist. Use /Z if you want to handle this case in your procedures rather than having execution abort. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Same as no /Z at all.</td></tr><tr><td>/Z=1:</td><td>Moves a file only if it exists. /Z alone is equivalent to /Z=1.</td></tr><tr><td>/Z=2:</td><td>Moves a file if it exists or displays a dialog if it does not exist.</td></tr></tbody></table>

### *Variables* {#variables}

|  |  |
| --- | --- |
| The MoveFile operation returns information in the following variables: |  |
| V_flag | Set to zero if the file was moved, to -1 if the user cancelled either the Open File or Save File dialogs, and to some nonzero value if an error occurred, such as the specified file does not exist. |
| S_fileName | Stores the full path to where the file was moved from. If an error occurred or if the user cancelled, it is set to an empty string. |
| S_path | Stores the full path where the file was moved to. If an error occurred or if the user cancelled, it is set to an empty string. |

### *Examples* {#examples}

```igor
// Rename a file, using full paths
MoveFile "HD:folder:aFile.txt" as "HD:folder:bFile.txt"

// Rename a file, using a symbolic path
MoveFile/P=myPath "aFile.txt" as "bFile.txt"

// Move a file into a subfolder (the subfolder must exist)
MoveFile/D "Macintosh HD:folder:aFile.txt" as ":subfolder"

// Move a file into an unrelated folder (the subfolder must exist)
MoveFile/D "Macintosh HD:folder:afile.txt" as "Server:archive"

// Move a file from one folder to another and rename it.
MoveFile "Macintosh HD:folder:afile.txt" as "Server:archive:destFile.txt"

// Move user-selected file into a particular folder
MoveFile/D as "C:My Data:Selected Files Folder"

// Move user-selected file in any folder as bFile.txt in same folder
MoveFile as "bFile.txt"

// Move user-selected file in any folder as bFile.txt in any folder
MoveFile/I=2 as "bFile.txt"
```

### *See Also* {#see-also}
[Operations[Open]](/igorpro/commands/open.md), [MoveFolder](/igorpro/commands/movefolder.md), [CopyFolder](/igorpro/commands/copyfolder.md), [NewPath](/igorpro/commands/newpath.md), [CreateAliasShortcut](/igorpro/commands/createaliasshortcut.md), [IndexedFile](/igorpro/commands/indexedfile.md), [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths)