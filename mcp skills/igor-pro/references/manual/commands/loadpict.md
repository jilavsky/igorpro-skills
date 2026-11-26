---
description: "The LoadPICT operation loads a picture from a file or from the Clipboard into Igor."
slug: /commands/loadpict
---

<div className="command-signature">

## <strong>LoadPICT</strong>  [/M=<em>promptStr</em> /O /P=<em>pathName</em> /Q /Z] [<em>fileNameStr</em> ] [, <em>pictName</em> ] {#loadpict}

</div>

The LoadPICT operation loads a picture from a file or from the Clipboard into Igor. Once you have loaded a picture, you can append it to graphs and page layouts.

### *Parameters* {#parameters}
The file to be loaded is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If Igor cannot determine the location of the file from *fileNameStr* and *pathName*, it displays a dialog allowing you to specify the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

If you want to force a dialog to select the file, omit the *fileNameStr* parameter.

If *fileNameStr* is "Clipboard" and /P=*pathName* is omitted, LoadPICT loads its data from the Clipboard rather than from a file.

*pictName* is the name that you want to give to the newly loaded picture. You can refer to the picture by its name to append it to graphs and page layouts. LoadPICT generates an error if the name conflicts with some other type of object (e.g., wave or variable) or if the name conflicts with a built-in name (e.g., the name of an operation or function).

If you omit *pictName*, LoadPICT automatically names the picture as explained in the Details section below.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/M = *promptStr*</span> | Specifies a prompt to use if LoadPICT needs to put up a dialog to find the file. |
| <span class="table-cell-nowrap">/O</span> | Overwrites an existing picture with the same name. |
|  | If /O is omitted and there is an existing picture with the same name, LoadPICT displays a dialog in which you can resolve the name conflict. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the file. *pathName* is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/Q</span> | Quiet mode: suppresses the insertion of picture info into the history area. |
| <span class="table-cell-nowrap">/Z</span> | Doesn't actually load the picture, just checks for its existence. |

### *Details* {#details}
If the picture file is not fully specified then LoadPICT presents a dialog from which you can select the file. "Fully specified" means that LoadPICT can determine the name of the file (from the *fileNameStr* parameter) and the folder containing the file (from the flag /P=*pathName* flag or from the *fileNameStr* parameter). If you want to force a dialog, omit the *fileNameStr* parameter.

If you use /P=*pathName* , note that it is the name of an Igor symbolic path, created via [NewPath](/igorpro/commands/newpath.md). It is not a file system path like "hd:Folder1:" or "C:\\Folder1\\". See [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths) for details.

If you omit *pictName*, LoadPICT automatically names the picture as follows:

If the picture was loaded from a file, LoadPICT uses the file name. If necessary, it makes it into a legal name by replacing illegal characters or shortening it.

Otherwise, LoadPICT uses a name of the form "PICT_*n* ".

If the resulting name is in conflict with an existing picture name, Igor puts up a name conflict resolution dialog.

LoadPICT sets the variable V_flag to 1 if the picture exists and fits in available memory or to 0 otherwise.

It also sets the string variable S_info to a semicolon-separated list of values:


| Keyword | Information Following Keyword |
| --- | --- |
| NAME | The name of the loaded pict, often "PICT_0", etc. |
| SOURCE | "Data fork" or "Clipboard". |
| RESOURCENAME | Obsolete - always "". |
| RESOURCEID | Obsolete - always 0. |
| TYPE | One of the following types: |
|  | DIB |
|  | Encapsulated PostScript |
|  | Enhanced metafile |
|  | JPEG |
|  | PDF |
|  | PNG |
|  | SVG |
|  | TIFF |
|  | Windows bitmap |
|  | Windows metafile |
|  | Unknown type |
| BYTES | Amount of memory used by the picture. |
| WIDTH | Width of the picture in pixels. |
| HEIGHT | Height of the picture in pixels. |
| PHYSWIDTH | Physical width of the picture in points. |
| PHYSHEIGHT | Physical height of the picture in points. |



### *See Also* {#see-also}
The [ImageLoad](/igorpro/commands/imageload.md) operation for loading PICT and other image file types into waves, and the [PICTInfo](/igorpro/commands/pictinfo.md) function.

[Pictures](/igorpro/graphing/making-figures/graphics.md#pictures)