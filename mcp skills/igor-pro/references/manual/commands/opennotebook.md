---
description: "The OpenNotebook operation opens a file for reading or writing as an Igor notebook."
slug: /commands/opennotebook
---

<div className="command-signature">

## <strong>OpenNotebook</strong>  [/A /ENCG=<em>textEncoding</em> /K=<em>k</em>  /M=<em>messageStr</em>  /N=<em>winName</em>  /P=<em>pathName</em> /R /T=<em>typeStr</em>  /V=<em>visible</em>  /W=(<em>left</em>,<em>top</em>,<em>right</em>,<em>bottom</em>) /Z] [<em>fileNameStr</em> ] {#opennotebook}

</div>

The OpenNotebook operation opens a file for reading or writing as an Igor notebook.

Unlike the Open operation, OpenNotebook will not create a file if the specified file does not exist. To create a new notebook, use the NewNotebook operation.

### *Parameters* {#parameters}
The file to be opened is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If Igor cannot determine the location of the file from *fileNameStr* and *pathName*, it displays a dialog allowing you to specify the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | The notebook's selection is moved to the end of the notebook. |
| <span class="table-cell-nowrap">/ENCG = *textEncoding*</span> | Specifies the text encoding of the plain text file to be opened as a notebook. |
|  | This flag was added in Igor Pro 7.00. |
|  | This is relevant for plain text notebooks only and is ignored for formatted notebooks because they can contain multiple text encodings. See [Plain Text File Text Encodings](/igorpro/igor-basics/text-encodings.md#plain-text-file-text-encodings) and [Formatted Text Notebook File Text Encodings](/igorpro/igor-basics/text-encodings.md#formatted-text-notebook-file-text-encodings) for details. |
|  | OpenNotebook uses the text encoding specified by /ENCG and the rules described under [Determining the Text Encoding for a Plain Text File](/igorpro/igor-basics/text-encodings.md#determining-the-text-encoding-for-a-plain-text-file) to determine the source text encoding for conversion to UTF-8. |
|  | Passing 0 for *textEncoding* acts as if /ENCG were omitted. |
|  | See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for a list of accepted values for *textEncoding*. |
| <span class="table-cell-nowrap">/K = *k*</span> | Specifies window behavior when the user attempts to close it. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr><tr><td>*k*&nbsp;=3:</td><td>Hides the window.</td></tr><tr><td>*k*&nbsp;=4:</td><td>Kills with no dialog and is not saved with the experiment.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/M = *messageStr*</span> | Prompt message text in the dialog used to find the file, if any. |
| <span class="table-cell-nowrap">/N = *winName*</span> | Specifies the window name to be assigned to the new notebook. If omitted, Igor assigns a name like "Notebook0". |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the file. *pathName* is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/R</span> | File is opened read only. |
| <span class="table-cell-nowrap">/T = *typeStr*</span> | Specifies the type or types of files that can be opened. |
| /V=*visible* |<table class="nested-table"><tbody><tr><td>*visible*&nbsp;=&nbsp;0:</td><td>Notebook will be initially hidden.</td></tr><tr><td>*visible*&nbsp;=&nbsp;1:</td><td>Notebook will be initially visible. This is the default.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom*)</span> |  |
|  | Specifies window size and position. Coordinates are in points. |
| <span class="table-cell-nowrap">/Z</span> | Suppresses error generation. Use this if you want to check if a file exists. If you use /Z, OpenNotebook sets the variable V_flag to 0 if the notebook was opened or to nonzero if there was an error, usually because the specified file does not exist. |

### *Details* {#details}
The /A (append) flag has no effect other than to move the selection to the end of the notebook after it is opened.

If you use /P=*pathName*, note that it is the name of an Igor symbolic path, created via [NewPath](/igorpro/commands/newpath.md). It is not a file system path like "hd:Folder1:" or "C:\\\\Folder1\\\\". See [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths) for details.

The /T=*typeStr* flag affects only the dialog that OpenNotebook presents if you do not specify a path and filename. The dialog presents only those files whose type is specified by /T=*typeStr*. There are two file types that are allowed for notebooks: 'TEXT' which is a plain text file and 'WMT0' which is a WaveMetrics formatted text file. Therefore, the file type, if you use it, should be either "TEXT" or "WMT0". If /T=*typeStr* is missing, it defaults to "TEXTWMT0". This opens either type of notebook file. On Windows, Igor considers files with ".txt" extensions to be of type TEXT and considers files with ".ifn" to be of type WMT0. See [File Types and Extensions](/igorpro/user-interface/platform-related-issues.md#file-types-and-extensions) for details.

### *See Also* {#see-also}
[Notebooks](/igorpro/igor-basics/notebooks.md), [Notebook](/igorpro/commands/notebook.md), [NewNotebook](/igorpro/commands/newnotebook.md)