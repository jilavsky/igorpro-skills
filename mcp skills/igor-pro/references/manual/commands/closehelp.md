---
description: "The CloseHelp operation closes a help window. The CloseHelp operation was added in Igor Pro 7.00."
slug: /commands/closehelp
---

<div className="command-signature">

## <strong>CloseHelp</strong>  [ /ALL /FILE=<em>fileNameStr</em>  /NAME=<em>helpNameStr</em>  /P=<em>pathName</em> ] {#closehelp}

</div>

The CloseHelp operation closes a help window.

The CloseHelp operation was added in Igor Pro 7.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALL</span> | Closes all open help windows. |
| <span class="table-cell-nowrap">/FILE = *fileNameStr*</span> |  |
|  | Identifies the help window to close using the help file's location on disk. The file is specified by *fileNameStr*  and /P=*pathName*  where *pathName*  is the name of an Igor symbolic path. *fileNameStr*  can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. |
|  | If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path. |
| <span class="table-cell-nowrap">/NAME = *helpNameStr*</span> |  |
|  | Identifies the help window to close using the window's title as specified by *helpNameStr* . This is the text that appears in the help window title bar. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the file specified by /FILE. *pathName*  is the name of an existing Igor symbolic path. |

### *Details* {#details}
You must provide one of the following flags: /ALL, /FILE, /NAME.

### *See Also* {#see-also}
[OpenHelp](/igorpro/commands/openhelp.md)