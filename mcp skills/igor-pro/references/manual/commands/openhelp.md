---
description: "The OpenHelp operation opens the specified help file. The OpenHelp operation was added in Igor Pro 7.00."
slug: /commands/openhelp
---

<div className="command-signature">

## <strong>OpenHelp</strong>  [<em>flags</em>] <em>fileNameStr</em> {#openhelp}

</div>

The OpenHelp operation opens the specified help file.

The OpenHelp operation was added in Igor Pro 7.00.

### *Parameters* {#parameters}
The help file to be opened is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If OpenHelp cannot determine the location of the file from *fileNameStr* and *pathName*, it returns an error.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/INT[ = *interactive*]</span> | Controls whether opening the help file is interactive or not. |
|  |<table class="nested-table"><tbody><tr><td>/INT=0:</td><td>If the help file being opened needs to be compiled, OpenHelp compiles it without presenting a dialog. Compilation errors are not presented to the user but are reflected in the V_Flag output variable.</td></tr><tr><td>/INT=1:</td><td>If the help file being opened needs to be compiled, OpenHelp presents a dialog asking the user whether the file should be compiled. During the compile, a progress dialog is displayed. Any errors are presented to the user in an error dialog. This is the default behavior if /INT is omitted.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the file. *pathName* is the name of an existing Igor symbolic path. |
| <span class="table-cell-nowrap">/PICT</span> | Scans the compiled help file for pictures and stores information about all pictures in a semicolon separated list into the S_pictureInfo output string. If the help file needs to be compiled but compilation fails, S_pictureInfo is set to "". |
| <span class="table-cell-nowrap">/V = *visible*</span> | Controls help window visibility. |
|  |<table class="nested-table"><tbody><tr><td>*visible*&nbsp;=&nbsp;0:</td><td>The help window will be initially hidden.</td></tr><tr><td>*visible*&nbsp;=&nbsp;1:</td><td>The help window will be initially visible. This is the default if /V is omitted.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom*)</span> |  |
|  | Specifies window size and position. Coordinates are in points. |
| <span class="table-cell-nowrap">/Z[ = z]</span> | Controls error reporting. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Report errors normally. /Z=0 is the same as omitting /Z altogether. This is the default behavior if /Z is omitted.</td></tr><tr><td>/Z=1:</td><td>Suppresses normal error reporting.</td></tr><tr><td></td><td>/Z alone has the same effect as /Z=1.</td></tr></tbody></table>
|  | /Z=1 prevents aborting procedure execution if an error occurs, for example if the file does not exist or if there is a compilation error. Use /Z=1 if you want to handle errors in your procedures rather than having execution abort. |
|  | When using /Z or /Z=1, check V_Flag to see if an error occurred. |

### *Details* {#details}
If you use /P=*pathName*, note that it is the name of an Igor symbolic path, created via [NewPath](/igorpro/commands/newpath.md). It is not a file system path like "hd:Folder1:" or "C:\\\\Folder1\\\\". See [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths) for details.

If the specified file is already open but not as a help window (for example as a notebook), OpenHelp returns an error.

If the /W or /V flag is used, or both, the window size and position and visibility are set as specified even if the file itself is already open, so long as the file is already opened as a help window.

### *Output Variables* {#output-variables}

The OpenHelp operation returns information in the following variables:

|  |  |
| --- | --- |
| V_Flag | Set to a non-zero value if an error occurred and to zero if no error occurred. |
| V_alreadyOpen | Set to 1 if the specified help file was already open as a help file or to zero otherwise. |
| S_pictureInfo | If you include the /PICT flag, OpenHelp sets S_pictureInfo to a semicolon-separated list of information for all pictures in the help file. If the help file needs to be compiled but compilation fails, S_pictureInfo is set to "". |

### *See Also* {#see-also}
[CloseHelp](/igorpro/commands/closehelp.md)