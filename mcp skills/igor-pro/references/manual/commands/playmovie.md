---
description: "The PlayMovie operation asks the operating system to open and play the specified movie."
slug: /commands/playmovie
---

<div className="command-signature">

## <strong>PlayMovie</strong>  [/I/M/P=<em>pathName</em> /Z] [<em>as</em> <em>fileNameStr</em> ] {#playmovie}

</div>

The PlayMovie operation asks the operating system to open and play the specified movie. If an application is registered with the operating system to play the movie, it is opened in that application, not directly within Igor.

### *Parameters* {#parameters}
The file to be opened is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If Igor cannot determine the location of the file from *fileNameStr* and *pathName*, it displays a dialog allowing you to specify the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/I</span> | This flag is obsolete and is ignored. |
| <span class="table-cell-nowrap">/M</span> | This flag is obsolete and is ignored. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the file. *pathName* is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom*)</span> | This flag is obsolete and is ignored. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting; an error is indicated by nonzero value of the variable V_flag. If the user clicks the cancel button in the Open File dialog, V_flag is set to -1. |

### *Details* {#details}
If the movie file to be played is not fully specified by /P and *fileNameStr*, PlayMovie displays an Open File dialog to let you choose a movie file. See [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths) and [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details.

### *See Also* {#see-also}
[Movies](/igorpro/advanced-topics.md#movies), [PlayMovieAction](/igorpro/commands/playmovieaction.md)