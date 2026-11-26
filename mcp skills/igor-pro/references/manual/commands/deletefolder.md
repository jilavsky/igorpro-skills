---
description: "The DeleteFolder operation deletes a disk folder and all of its contents."
slug: /commands/deletefolder
---

<div className="command-signature">

## <strong>DeleteFolder</strong>  [/I/M=<em>messageStr</em> /P=<em>pathName</em> /Z ]  [<em>folderNameStr</em>  ] {#deletefolder}

</div>

The DeleteFolder operation deletes a disk folder and all of its contents.

:::caution
The DeleteFolder command destroys data! The deleted folder and the contents are not moved to the Trash or Recycle Bin!

DeleteFolder will delete a folder only if permission is granted by the user. The default behavior is to display a dialog asking for permission. The user can alter this behavior via the Miscellaneous Settings dialog's Misc category.

If permission is denied, the folder will not be deleted and V_Flag will return 1088 (Command is disabled) or 1276 (You denied permission to delete a folder). Command execution will cease unless the /Z flag is specified.
:::

*folderNameStr*  can be a full path to the folder to be deleted, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a folder within the folder associated with *pathName*.

If Igor cannot determine the location of the folder from *folderNameStr*  and *pathName*, it displays a Select Folder dialog allowing you to specify the folder to be deleted.

If /P=*pathName*  is given, but *folderNameStr* is not, then the folder associated with *pathName* is deleted.

If you use a full or partial path for either folder, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

Folder paths should not end with single [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators). See [MoveFolder](/igorpro/commands/movefolder.md)'s Details section.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/I</span> | Interactive mode displays a Select Folder dialog even if *folderNameStr* is specified and the folder exists. |
| <span class="table-cell-nowrap">/M = *messageStr*</span> | Specifies the prompt message in the Select Folder dialog. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the folder. *pathName*  is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/Z[ = *z* ]</span> | Prevents procedure execution from aborting if it attempts to delete a folder that does not exist. Use /Z if you want to handle this case in your procedures rather than having execution abort. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Same as no /Z.</td></tr><tr><td>/Z=1:</td><td>Deletes a folder only if it exists. /Z alone has the same effect as /Z=1.</td></tr><tr><td>/Z=2:</td><td>Deletes a folder if it exists or displays a dialog if it does not exist.</td></tr></tbody></table>

### *Variables* {#variables}

|  |  |
| --- | --- |
| The DeleteFolder operation returns information in the following variables: |  |
| V_flag | Set to zero if the folder was deleted, to -1 if the user cancelled the Select Folder dialog, and to some nonzero value if an error occurred, such as the specified folder does not exist. |
| S_path | Stores the full path to the folder that was deleted, with a trailing colon. If an error occurred or if the user cancelled, it is set to an empty string. |

### *Details* {#details}
You can use only /P=*pathName* (without *folderNameStr*) to specify the source folder to be deleted.

Folder paths should not end with single [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators). See [MoveFolder](/igorpro/commands/movefolder.md)'s Details section.

### *See Also* {#see-also}
[DeleteFile](/igorpro/commands/deletefile.md), [MoveFolder](/igorpro/commands/movefolder.md), [CopyFolder](/igorpro/commands/copyfolder.md), [NewPath](/igorpro/commands/newpath.md), [IndexedDir](/igorpro/commands/indexeddir.md), [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths)