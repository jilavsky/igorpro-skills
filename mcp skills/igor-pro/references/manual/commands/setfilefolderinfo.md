---
description: "The SetFileFolderInfo operation changes a file's or folder's properties."
slug: /commands/setfilefolderinfo
---

<div className="command-signature">

## <strong>SetFileFolderInfo</strong>  [ /CDAT=<em>cDate</em> /CRE8=<em>creatorStr</em> /D /FTYP=<em>typeStr</em> /INV=<em>inv</em>  /MDAT=<em>mDate</em> /P=<em>pathName</em> /R=<em>r</em> /RO=<em>ro</em> /STA=<em>st</em> /UTC[=<em>u</em>] /Z=<em>z</em>] ] [<em>fileOrFolderNameStr</em>] {#setfilefolderinfo}

</div>

The SetFileFolderInfo operation changes a file's or folder's properties.

### *Parameters* {#parameters}
*fileOrFolderNameStr* specifies the file or folder to be changed.

If you use a full or partial path for *fileOrFolderNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

Folder paths should not end with single [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators). See [MoveFolder](/igorpro/commands/movefolder.md)'s Details section.

If Igor cannot determine the location of the file or folder from *fileOrFolderNameStr* and *pathName*, it displays a dialog allowing you to specify the file to be deleted. Use /D to select a folder in this event, otherwise Igor prompts your for a file.

### *Flags* {#flags}
**At least one of the four following flags is required, or nothing is actually accomplished:**


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/CDAT = *cDate*</span> | Specifies the number of seconds since midnight on January 1, 1904 when the file or folder was first created. *cDate* is interpreted as local time or UTC depending on the /UTC flag. |
| <span class="table-cell-nowrap">/INV[ = *inv* ]</span> | Sets the visibility of a file. |
|  |<table class="nested-table"><tbody><tr><td>*inv*&nbsp;=0:</td><td>File is visible.</td></tr><tr><td>*inv*&nbsp;=1:</td><td>Default; file is hidden.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/MDAT = *mDate*</span> | Specifies the number of seconds since midnight on January 1, 1904 when the file or folder was modified most recently. *mDate* is interpreted as local time or UTC depending on the /UTC flag. |
| <span class="table-cell-nowrap">/RO[ = *ro* ]</span> | Sets the read/write state of a file or folder. |
|  |<table class="nested-table"><tbody><tr><td>*ro*&nbsp;=0:</td><td>File or folder is writable.</td></tr><tr><td>*ro*&nbsp;=1:</td><td>File or folder is read-only (default).</td></tr></tbody></table>
| This is equivalent to setting the read-only property manually using the Properties window in Windows Explorer. |  |
| See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |  |

### *Optional Flags* {#optional-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D</span> | When *pathName* and *fileOrFolderNameStr* do not specify an existing file or folder, use the Select Folder dialog rather than Open File dialog. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the file. *pathName* is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/R[ = *r* ]</span> | Recursively applies change(s) to all files or folders in the folder specified by *pathName* or *fileOrFolderNameStr*, and the folder itself: |
|  |<table class="nested-table"><tbody><tr><td>*r*&nbsp;=0:</td><td>No recursion. Same as no /R.</td></tr><tr><td>*r*&nbsp;=1:</td><td>Recursively apply changes to files.</td></tr><tr><td>*r*&nbsp;=2:</td><td>Recursively apply changes to folders, including the folder specified by *pathName* or *fileOrFolderNameStr*.</td></tr><tr><td>*r*&nbsp;=3:</td><td>Recursively apply changes to both files and folders (default).</td></tr></tbody></table>
|  | /R requires /D and a folder specification. |
| <span class="table-cell-nowrap">/UTC[ = *u* ]</span> | If you include /UTC or /UTC=1, SetFileFolderInfo interprets the creation and modification dates as UTC (coordinated universal time). If you omit /UTC or specify /UTC=0, SetFileFolderInfo interprets the creation and modification dates as local time. |
|  | The default, used if you omit /UTC, is local time. |
|  | The /UTC flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/Z[ = *z* ]</span> | Prevents procedure execution from aborting if SetFileFolderInfo tries to set information about a file or folder that does not exist. Use /Z if you want to handle this case in your procedures rather than having execution abort. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Same as no /Z at all.</td></tr><tr><td>/Z=1:</td><td>Used for setting information for a file or folder only if it exists. /Z alone has the same effect as /Z=1.</td></tr><tr><td>/Z=2:</td><td>Used for setting information for a file or folder if it exists and displaying a dialog if it does not exist.</td></tr></tbody></table>

### *Variables* {#variables}
SetFileFolderInfo returns information about the file or folder in the following variables:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the file or folder was found, to -1 if the user cancelled the Open File dialog, and to some nonzero value if an error occurred, such as the specified file or folder does not exist. |
| S_Path | Set to the file system path of the selected file or folder. |

### *Examples* {#examples}

```igor
// Set a file's modification date and time
Variable hrs = 12, mins = 30, secs = 15 // 12:30:15
Variable mDate= Date2Secs(2000,12,25) + hrs*3600+mins*60+secs
SetFileFolderInfo/P=myPath/MDAT=(mDate), "afile.txt"

// Remove read-only property from a folder and everything within it:
SetFileFolderInfo/P=myPath/D/R/RO=0
```

### *See Also* {#see-also}
[GetFileFolderInfo](/igorpro/commands/getfilefolderinfo.md), [FStatus](/igorpro/commands/fstatus.md), [IndexedFile](/igorpro/commands/indexedfile.md), [Date2Secs](/igorpro/commands/date2secs.md), [ParseFilePath](/igorpro/commands/parsefilepath.md)