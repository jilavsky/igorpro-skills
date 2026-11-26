---
description: "The NewPath operation creates a new symbolic path name that can be used as a shortcut to refer to a folder on disk."
slug: /commands/newpath
---

<div className="command-signature">

## <strong>NewPath</strong>  [/C/M=<em>messageStr</em> /O/Q/Z] <em>pathName</em>  [, <em>pathToFolderStr</em>] {#newpath}

</div>

The NewPath operation creates a new symbolic path name that can be used as a shortcut to refer to a folder on disk.

### *Parameters* {#parameters}
*pathToFolderStr* is a string containing the path to the folder for which you want to make a symbolic path. *pathToFolderStr* can also point to a shortcut for a folder.

If you use a full path for *pathToFolderStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path. If you use a partial path or just a simple name for *pathToFolderStr*, and you use the /C flag, a new folder is created relative to the Igor Pro folder. No dialog is presented.

If you omit *pathToFolderStr*, you get a chance to select a folder or create a new folder from a dialog.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C</span> | The folder specified by "path" is created if it does not already exist. |
| <span class="table-cell-nowrap">/M = *messageStr*</span> | Specifies the prompt message in the dialog. |
| <span class="table-cell-nowrap">/O</span> | Overwrites the symbolic path if it exists. |
| <span class="table-cell-nowrap">/Q</span> | Suppresses printing path information in the history |
| <span class="table-cell-nowrap">/Z</span> | Doesn't generate an error if the folder does not exist. |

### *Details* {#details}
Symbolic paths help to isolate your experiments from specific file system paths that contain files created or used by Igor. By using a symbolic path, if the actual location or name of the folder changes, you won't need to change all of your commands. Instead, you need only to change the symbolic path so that it points to the changed folder location.

NewPath sets the variable V_flag to zero if the operation succeeded or to nonzero if it failed. The main use for this is to determine if the user clicked Cancel when you use NewPath to display a choose-folder dialog.

### *Examples* {#examples}
For example:

```igor
NewPath Path1, "C:IgorStuff:Test 1"
```

creates the symbolic path named Path1 which refers to the specified folder (the path's "value"). You can then refer to this folder in many Igor operations and dialogs by using the symbolic path name Path1.

:::note
Due to Igor's history, you can use either the colon or the backslash character to separate folders. However, the backslash character is Igor's escape character in strings. This means that you have to double each backslash to get one backslash:
:::

```igor
NewPath stuff, "C:\\IgorStuff\\Test 1"
```

> Because of this complication, it is recommended that you use colons as separators. See Path Separators for details.

### *See Also* {#see-also}
[Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths), [PathInfo](/igorpro/commands/pathinfo.md), [KillPath](/igorpro/commands/killpath.md)