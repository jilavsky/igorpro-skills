---
description: "The CreateAliasShortcut operation creates a shortcut file on disk. The shortcut can point to either a file or a folder."
slug: /commands/createaliasshortcut
---

<div className="command-signature">

## <strong>CreateAliasShortcut</strong>  [/D/I[=<em>i</em> ]/M=<em>messageStr</em> /O/P=<em>pathName</em> /S=<em>saveMessageStr</em> /Z[=<em>z</em> ] ]  [<em>targetFileDirStr</em> ]  [ <em>as</em> <em>shortcutFileStr</em> ] {#createaliasshortcut}

</div>

The CreateAliasShortcut operation creates a shortcut file on disk. The shortcut can point to either a file or a folder. The file or folder pointed to is called the "target" of the shortcut.

Before Igor 10, Igor Macintosh versions supported aliases, which are equivalent to Windows shortcuts.

### *Parameters* {#parameters}
*targetFileDirStr*  can be a full path to the file or folder to make a shortcut for, a partial path relative to the folder associated with /P=*pathName*, or the name of a file or folder in the folder associated with *pathName*.

If Igor cannot determine the location of the file or folder from *targetFileDirStr* and *pathName*, it displays a dialog allowing you to specify a target file. Use /D to select a folder as the shortcut target, instead.

*shortcutFileStr* can be a full path to the created shortcut file, a partial path relative to the folder associated with *pathName* if specified, or the name of a file in the folder associated with *pathName*.  Both Windows-formatted and Macintosh-formated file paths are supported.

If Igor cannot determine the location of the shortcut file from *shortcutFileStr* and *pathName*, it displays a File Save dialog allowing you to create the file.

If you use a full or partial path for either *targetFileDirStr* or *shortcutFileStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

Folder paths should not end with single [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators). See [MoveFolder](/igorpro/commands/movefolder.md)'s Details section.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D</span> | Use the Select Folder dialog rather than Open File dialog when *targetFileDirStr* is not fully specified. |
| <span class="table-cell-nowrap">/I[ = *i* ]</span> | Specifies the level of user interactivity. |
|  |<table class="nested-table"><tbody><tr><td>*i*&nbsp;=0:</td><td>Interactive only if one or *targetFileDirStr* or *shortcutFileStr* is not specified or if the target file is missing. (Same as if /I was not specified.)</td></tr><tr><td>*i*&nbsp;=1:</td><td>Interactive even if *targetFileDirStr* is fully specified and the target file exists.</td></tr><tr><td>*i*&nbsp;=2:</td><td>Interactive even if *targetFileDirStr* is specified.</td></tr><tr><td>*i*&nbsp;=3:</td><td>Interactive even if *targetFileDirStr* is specified and the target file exists. Same as /I only.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/M = *messageStr*</span> | Specifies the prompt message in the Open File or Select Folder dialog.  If /S is not specified, then *messageStr*  will be used for Open File (or Select Folder) and for Save File dialogs. |
| <span class="table-cell-nowrap">/O</span> | Overwrites any existing file with the shortcut file. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the file. *pathName*  is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/S = *saveMessageStr*</span> | Specifies the prompt message in the Save File dialog when creating the shortcut file. |
| <span class="table-cell-nowrap">/Z[ = *z* ]</span> | Prevents procedure execution from aborting if the procedure tries to create a shortcut for a file or folder that does not exist. Use /Z if you want to handle this case in your procedures rather than having execution abort. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Same as no /Z at all.</td></tr><tr><td>/Z=1:</td><td>Creates a shortcut to a file or folder only if it exists. /Z alone has the same effect as /Z=1.</td></tr><tr><td>/Z=2:</td><td>Creates a shortcut to a file or folder only if it exists and displays a dialog if it does not exist.</td></tr></tbody></table>

### *Variables* {#variables}

|  |  |
| --- | --- |
| The CreateAliasShortcut operation returns information in the following variables: |  |
| V_Flag |<table class="nested-table"><tbody><tr><td>0:</td><td>Created a shortcut file.</td></tr><tr><td>-1:</td><td>User cancelled any of the Open File, Select Folder, or Save File dialogs.</td></tr><tr><td>Other:</td><td>An error occurred, such as the target file does not exist.</td></tr></tbody></table>
| S_path | Full path to the created shortcut file. If an error occurred or if the user cancelled, it is an empty string. |
| S_fileName | Full path to the target file or folder. If an error occurred or if the user cancelled, it is an empty string. |

### *Examples* {#examples}

```igor
// Create a shortcut to the current experiment on the Desktop
String target= Igorinfo(1)+".pxp"	// experiment files have .pxp extensions
CreateAliasShortcut/O/P=home target as "C:\\Users\\myName\\Desktop\\"+target // explicit Windows file path style
Print S_fileName	// Full path to target (Mac file path style)
Print S_path		// Full path to the created shortcut file (Mac file path style)

// Same example using Mac file path style returned from SpecialDirPath
String desktopPath = SpecialDirPath("Desktop", 0, 0, 0) // mac file path with ending ":" separator
String shortcutPath = desktopPath+target
CreateAliasShortcut/O/P=home target as shortcutPath
Print S_fileName	// Full path to target (Mac file path style)
Print S_path		// Full path to the created shortcut file (Mac file path style)

// Reveal the desktop in Windows Explorer
NewPath/O/Q Desktop, desktopPath
PathInfo/SHOW Desktop
```

### *See Also* {#see-also}
[Open](/igorpro/commands/open.md), [MoveFile](/igorpro/commands/movefile.md), [DeleteFile](/igorpro/commands/deletefile.md), [GetFileFolderInfo](/igorpro/commands/getfilefolderinfo.md), [IgorInfo](/igorpro/commands/igorinfo.md), [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths), [ParseFilePath](/igorpro/commands/parsefilepath.md)