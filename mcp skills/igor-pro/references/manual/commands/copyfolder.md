---
description: "The CopyFolder operation copies a folder (and its contents) on disk. The CopyFolder command can destroy data by overwriting another folder and contents!"
slug: /commands/copyfolder
---

<div className="command-signature">

## <strong>CopyFolder</strong>  [/D/I[=<em>i</em> ]/M=<em>messageStr</em> /O/P=<em>pathName</em> /S=<em>saveMessageStr</em> /Z [=<em>z</em> ] ]  [<em>srcFolderStr</em> ]  [ <em>as</em> <em>destFolderStr</em> ] {#copyfolder}

</div>

The CopyFolder operation copies a folder (and its contents) on disk.

:::caution
The CopyFolder command can destroy data by overwriting another folder and contents!

When overwriting an existing folder on disk, CopyFolder will do so only if permission is granted by the user. The default behavior is to display a dialog asking for permission. The user can alter this behavior via the Miscellaneous Settings dialog's Misc category.

If permission is denied, the folder will not be copied and V_Flag will return 1088 (Command is disabled) or 1275 (You denied permission to overwrite a folder). Command execution will cease unless the /Z flag is specified.
:::

*srcFolderStr*  can be a full path to the folder to be copied (in which case /P is not needed), a partial path relative to the folder associated with *pathName*, or the name of a folder inside the folder associated with *pathName*.

If Igor cannot determine the location of the folder from *srcFolderStr*  and *pathName*, it displays a dialog allowing you to specify the source folder.

If /P=*pathName*  is given, but *srcFolderStr* is not, then the folder associated with *pathName*  is copied.

*destFolderStr*  can be a full path to the output (destination) folder (in which case /P is not needed), or a partial path relative to the folder associated with *pathName*.

An error is returned if the destination folder would be inside the source folder.

If Igor cannot determine the location of the destination folder from *destFolderStr*  and *pathName*, it displays a dialog allowing you to specify or create the destination folder.

If you use a full or partial path for either folder, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D</span> | Interprets *destFolderStr*  as the name of (or path to) an existing folder (or "directory") to copy the source folder into. Without /D, *destFolderStr* is interpreted as the name of (or path to) the copied folder. |
|  | If *destFolderStr* is not a full path to a folder, it is relative to the folder associated with *pathName*. |
| <span class="table-cell-nowrap">/I[ = *i* ]</span> | Specifies the level of interactivity with the user. |
|  |<table class="nested-table"><tbody><tr><td>*i*&nbsp;=0:</td><td>Interactive only if the source or destination folder is not specified or if the source folder is missing. (Same as if /I was not specified.)</td></tr><tr><td>*i*&nbsp;=1:</td><td>Interactive even if the source folder is specified and it exists.</td></tr><tr><td>*i*&nbsp;=2:</td><td>Interactive even if *destFolderStr* is specified.</td></tr><tr><td>*i*&nbsp;=3:</td><td>Interactive even if the source folder is specified, the source file exists, and *destFolderStr* is specified. Same as /I only.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/M = *messageStr*</span> | Specifies the prompt message in the Select (source) Folder dialog.  If /S is not specified, then *messageStr*  will be used for the Select Folder dialog and for the Create Folder dialog. |
| <span class="table-cell-nowrap">/O</span> | Overwrite existing destination folder, if any. |
|  | A Windows-style mix-in move is performed in which the contents of the source folder are moved into the destination folder, replacing any same-named files but leaving other files in place. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the source folder. *pathName*  is the name of an existing symbolic path. |
|  | If *srcFolderStr* is not specified, the folder associated with *pathName* is copied. |
|  | Using /P means that *srcFolderStr* (if specified) and *destFolderStr* must be either simple folder names or paths relative to the folder specified by *pathName*. |
| <span class="table-cell-nowrap">/S = *saveMessageStr*</span> | Specifies the prompt message in the Create Folder dialog. |
| <span class="table-cell-nowrap">/Z[ = *z* ]</span> | Prevent procedure execution from aborting if it attempts to copy a file that does not exist. Use /Z if you want to handle this case in your procedures rather than having execution abort. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Same as no /Z at all.</td></tr><tr><td>/Z=1:</td><td>Copies a folder only if it exists. /Z alone has the same effect as /Z=1.</td></tr><tr><td>/Z=2:</td><td>Copies a folder if it exists or displays a dialog if it does not exist.</td></tr></tbody></table>

### *Variables* {#variables}

|  |  |
| --- | --- |
| The CopyFolder operation returns information in the following variables: |  |
| V_flag | Set to zero if the folder was copied, to -1 if the user cancelled either the Select Folder or Create Folder dialogs, and to some nonzero value if an error occurred, such as the specified file does not exist. |
| S_fileName | Stores the full path to the folder that was copied, with a trailing colon. If an error occurred or if the user cancelled, it is set to an empty string. |
| S_path | Stores the full path to the folder copy, with a trailing colon. If an error occurred or if the user cancelled, it is set to an empty string. |

### *Details* {#details}
You can use only /P=pathName (without *srcFolderStr*) to specify the source folder to be copied.

Folder paths should not end with single [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators). See [MoveFolder](/igorpro/commands/movefolder.md)'s Details section.

### *See Also* {#see-also}
[Open](/igorpro/commands/open.md), [MoveFile](/igorpro/commands/movefile.md), [DeleteFile](/igorpro/commands/deletefile.md), [MoveFolder](/igorpro/commands/movefolder.md), [NewPath](/igorpro/commands/newpath.md), [IndexedDir](/igorpro/commands/indexeddir.md), [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths)