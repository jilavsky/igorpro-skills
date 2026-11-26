---
description: "The MoveFolder operation moves or renames a folder on disk. A folder is renamed by \"moving\" it into the same folder it is already in, but with a different name."
slug: /commands/movefolder
---

<div className="command-signature">

## <strong>MoveFolder</strong>  [/D /I[=<em>i</em>]/M=<em>messageStr</em> /O/P=<em>pathName</em> /S=<em>saveMessageStr</em> /Z[=<em>z</em> ] ]  [<em>srcFolderStr</em> ]  [ <em>as</em> <em>destFolderStr</em> ] {#movefolder}

</div>

The MoveFolder operation moves or renames a folder on disk.  A folder is renamed by "moving" it into the same folder it is already in, but with a different name.

:::caution
The MoveFolder command can destroy data by overwriting another folder and contents!
:::

> If you overwrite an existing folder on disk, MoveFolder will do so only if permission is granted by the user. The default behavior is to display a dialog asking for permission. The user can alter this behavior via the Miscellaneous Settings dialog's Misc category.

> If permission is denied, the folder will not be moved and V_Flag will return 1088 (Command is disabled) or 1275 (You denied permission to overwrite a folder). Command execution will cease unless the /Z flag is specified.

### *Parameters* {#parameters}

*srcFolderStr* can be a full path to the folder to be moved or renamed (in which case /P is not needed), a partial path relative to the folder associated with *pathName*, or the name of a folder within the folder associated with *pathName*.

If Igor cannot determine the location of the source folder from *srcFolderStr* and *pathName*, it displays a Select Folder dialog allowing you to specify the source.

If /P=*pathName* is given, but *srcFolderStr* is not, then the folder associated with *pathName* is moved or renamed.

*destFolderStr* specifies the final location of the folder or, if /D is used, the parent of the final location of the folder.

*destFolderStr* can be a full path to the output (destination) folder (in which case /P is not needed), or a partial path relative to the folder associated with *pathName*.

If Igor cannot determine the location of the destination folder from *destFolderStr* and *pathName*, it displays a Save Folder dialog allowing you to specify the destination.

If you use a full or partial path for either file, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D</span> | *destFolderStr* is interpreted as the name of (or path to) an existing folder (or "directory") to move the source folder into. Without /D, *destFolderStr* is interpreted as the name of (or path to) the moved folder. |
|  | If *destFolderStr* is not a full path to a folder, it is relative to the source folder. |
| /I [=*i* ] |<table class="nested-table"><tbody><tr><td>*i*&nbsp;=0:</td><td>Interactive only if *srcFolderStr* or *destFolderStr* is not specified or if the source folder is missing. (Same as if /I was not specified.)</td></tr><tr><td>*i*&nbsp;=1:</td><td>Interactive even if *srcFolderStr* is specified and the source folder exists.</td></tr><tr><td>*i*&nbsp;=2:</td><td>Interactive even if *destFolderStr* is specified.</td></tr><tr><td>*i*&nbsp;=3:</td><td>Interactive even if *srcFolderStr* is specified and the source folder exists. Same as /I only.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/M = *messageStr*</span> | Specifies the prompt message in the Open File dialog.  If /S is not specified, then *messageStr* will be used for both Open File and for Save File dialogs. |
| <span class="table-cell-nowrap">/O</span> | Overwrite existing destination folder, if any. This deletes the existing destination folder. When /O is specified, the source folder can't be moved into an existing folder without specifying the name of the moved folder in *destFolderStr*. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | *pathName* is the name of an existing symbolic path. |
|  | Specifies the folder for relative paths in *srcFolderStr* and *destFolderStr*. If *srcFolderStr* is omitted, the folder associated with *pathName* is moved. If *destFolderStr* is omitted, the source folder is moved into the folder associated with *pathName*. |
|  | Using /P means that *srcFolderStr* (if specified) and *destFolderStr* must be either simple folder names or paths relative to the folder specified by *pathName*. |
| <span class="table-cell-nowrap">/S = *saveMessageStr*</span> | Specifies the prompt message in the Save File dialog. |
| <span class="table-cell-nowrap">/Z[ = *z* ]</span> | Prevents procedure execution from aborting if it attempts to move a folder that does not exist. Use /Z if you want to handle this case in your procedures rather than having execution abort. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Same as no /Z at all.</td></tr><tr><td>/Z=1:</td><td>Moves a folder only if it exists. /Z alone is equivalent to /Z=1.</td></tr><tr><td>/Z=2:</td><td>Moves a folder if it exists or displays a dialog if it does not exist.</td></tr></tbody></table>

### *Variables* {#variables}
The MoveFolder operation returns information in the following variables:


|  |  |
| --- | --- |
| V_flag | Set to zero if the file was moved, to -1 if the user cancelled either the Open File or Save File dialogs, and to some nonzero value if an error occurred, such as the specified file does not exist. |
| S_fileName | Stores the full path to the folder that was moved, with a trailing colon. If an error occurred or if the user cancelled, it is set to an empty string. |
| S_path | Stores the full path of the moved folder, with a trailing colon. If an error occurred or if the user cancelled, it is set to an empty string. |

### *Details* {#details}
You can use /P=*pathName* alone (omitting *srcFolderStr*) to specify the source folder to be moved.

A folder may not be moved into one of its own subfolders.

Conversely, the command:


```igor
MoveFolder/O/P=myPath "afolder"
```

which attempts to overwrite the folder associated with myPath with a folder that is inside it (namely "afolder") is not allowed. Instead, use:


```igor
MoveFolder/O/P=myPath "::afolder"
```

On Windows, renaming or moving a folder never updates the value of any Igor [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths) that point to a moved folder:


```igor
// Create a folder
NewPath/O/C myPath "C:\\My Data\\My Work"

// Move the folder
MoveFolder/P=myPath as "C:\\My Data\\Moved"

// Display the path's value
PathInfo myPath	//  (or use the Path Status dialog)
Print S_Path
	C:My Data:My Work
```

You can use [PathInfo](/igorpro/commands/pathinfo.md) to determine if a folder referred to by an Igor symbolic path exists and where it is on the disk. Use [NewPath](/igorpro/commands/newpath.md)/O to reset the path's value.

Moving the folder to a different volume actually creates a new folder with new volume refnum and directory IDs, and symbolic paths pointing to or into the moved folder aren't updated. They will be pointing at a deleted folder (they're probably invalid).

### *Examples* {#examples}

```igor
// Rename a folder ("move" it to the same folder)
MoveFolder "C:Users:jim:Documents:Subfolder" as "C:Users:jim:Documents:Subfolder Renamed"

// Rename a folder referred to by only a path name (myPath).
// Create the symbolic path name for full path to my Documents\Subfolder
String docs = SpecialDirPath("Documents", 0, 0, 0) // has trailing ":", Macintosh format
String pathToFolder = docs+"Subfolder" // no trailing ":"
NewPath/O/Q myPath, pathToFolder
MoveFolder/P=myPath as "::Subfolder Renamed"

// Move a folder from one volume to another, renaming the moved folder
// This moves F:\:Test Data inside my Documents\Subfolder folder.
// Without /D the destFolderStr is the name of the moved folder.
MoveFolder "F:\\Test Data" as "C:\\Users\\jim\\Documents\\Subfolder\\Moved Test Data"

// Move a folder from one volume to another.
// This moves F:\:Test Data inside my Documents\Subfolder folder.
// The /D flag is used to move Test Data without renaming the moved folder. 
MoveFolder/D "F:\\Test Data" as "C:\\Users\\jim\\Documents\\Subfolder"

// Move a folder's contents from one volume to another.
// On Windows, /O MERGES the contents of F:\Test Data with an existing Moved Text Data folder.
// On Macintosh /O REPLACES the entire Moved Test Data folder (if it existed) with the moved Test Data and contents.
// Before overwriting (whether merging or replacing),  the user is prompted for permission unless disabled in Misc Settings.
MoveFolder/O "F:\\Test Data" as "C:\\Users\\jim\\Documents\\Subfolder\\Moved Test Data"

// Move user-selected folder in any folder as "Renamed Folder"
// into a user-selected folder (possibly the same one)
MoveFolder as "Renamed Folder"

// Move user-selected file in any folder as "Moved Folder"
// in any folder
MoveFolder/I=3 as "Moved Folder"
```

### *See Also* {#see-also}
[MoveFile](/igorpro/commands/movefile.md), [CopyFolder](/igorpro/commands/copyfolder.md), [DeleteFolder](/igorpro/commands/deletefolder.md), [IndexedDir](/igorpro/commands/indexeddir.md), [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths), [PathInfo](/igorpro/commands/pathinfo.md), [RemoveEnding](/igorpro/commands/removeending.md), [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators)