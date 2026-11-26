---
description: "The DeleteFile operation deletes a file on disk. fileNameStr can be a full path to the file to be deleted (in which case /P is not needed), a partial path…"
slug: /commands/deletefile
---

<div className="command-signature">

## <strong>DeleteFile</strong>  [/I/M=<em>messageStr</em> /P=<em>pathName</em>  /Z ]  [<em>fileNameStr</em>  ] {#deletefile}

</div>

The DeleteFile operation deletes a file on disk.

### *Parameters* {#parameters}
*fileNameStr*  can be a full path to the file to be deleted (in which case /P is not needed), a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*.

If Igor cannot determine the location of the file from *fileNameStr*  and *pathName*, it displays a dialog allowing you to specify the file to be deleted.

If you use a full or partial path for either file, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/I</span> | Interactive mode. The Open File dialog will display even if *fileNameStr* is specified and the file exists. |
| <span class="table-cell-nowrap">/M = *messageStr*</span> | Specifies the prompt message in the Open File dialog. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the file. *pathName*  is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/Z[ = *z* ]</span> | Prevents procedure execution from aborting if it attempts to delete a file that does not exist. Use /Z if you want to handle this case in your procedures rather than having execution abort. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Same as no /Z.</td></tr><tr><td>/Z=1:</td><td>Deletes a file only if it exists. /Z alone has the same effect as /Z=1.</td></tr><tr><td>/Z=2:</td><td>Deletes a file if it exists or displays a dialog if it does not exist.</td></tr></tbody></table>

### *Variables* {#variables}

|  |  |
| --- | --- |
| The Delete operation returns information in the following variables: |  |
| V_flag | Set to zero if the file was deleted, to -1 if the user cancelled the Open File dialog, and to some nonzero value if an error occurred, such as the specified file does not exist. |
| S_path | Stores the full path to the file that was deleted.  If an error occurred or if the user cancelled, it is set to an empty string. |

### *See Also* {#see-also}
[DeleteFolder](/igorpro/commands/deletefolder.md), [MoveFile](/igorpro/commands/movefile.md), [CopyFile](/igorpro/commands/copyfile.md), [NewPath](/igorpro/commands/newpath.md), [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths)