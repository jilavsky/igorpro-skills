---
description: "The OpenProc operation opens a file as an Igor procedure file. This operation is used automatically by Igor to open procedure files when you open an Igor…"
slug: /commands/openproc
---

<div className="command-signature">

## <strong>OpenProc</strong>   [<em>flags</em> ] [<em>fileNameStr</em> ] {#openproc}

</div>

The OpenProc operation opens a file as an Igor procedure file.

:::note
This operation is used automatically by Igor to open procedure files when you open an Igor experiment. You can invoke OpenProc only from the command line. Do not invoke it from a procedure. To open procedure files from a procedure or from a menu definition, use the Execute/P operation.
:::

### *Parameters* {#parameters}

The file to be opened is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If Igor cannot determine the location of the file from *fileNameStr* and *pathName*, it displays a dialog allowing you to specify the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Procedure window's selection is moved to the end of the window. |
| <span class="table-cell-nowrap">/ENCG = *textEncoding*</span> | Specifies the text encoding of the plain text file to be opened as a procedure file. |
|  | This flag was added in Igor Pro 7.00. |
|  | OpenProc uses the text encoding specified by /ENCG and the rules described under [Determining the Text Encoding for a Plain Text File](/igorpro/igor-basics/text-encodings.md#determining-the-text-encoding-for-a-plain-text-file) to determine the source text encoding for conversion to UTF-8. |
|  | Passing 0 for *textEncoding* acts as if /ENCG were omitted. |
|  | See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for a list of accepted values for *textEncoding*. |
| <span class="table-cell-nowrap">/M = *messageStr*</span> | Prompt message text in the dialog used to find the file, if any. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the file. *pathName* is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/R</span> | File is opened read only. |
| <span class="table-cell-nowrap">/T = *typeStr*</span> | Specifies the type or types of files that can be opened. |
| /V=*visible* |<table class="nested-table"><tbody><tr><td>*visible*=&nbsp;0:</td><td>Procedure window will be initially hidden.</td></tr><tr><td>*visible*=&nbsp;1:</td><td>Window will be initially visible. This is the default.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Suppresses error generation if the specified file does not exist. |

### *Details* {#details}
The /A (append) flag has no effect other than to move the selection to the end of the procedure file after it is opened.

If you use /P=*pathName*, note that it is the name of an Igor symbolic path, created via [NewPath](/igorpro/commands/newpath.md). It is not a file system path like "hd:Folder1:" or "C:\\\\Folder1\\\\". See [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths) for details.

This operation automatically opens procedure files when you open an Igor experiment. Normally, you will have no use for it. You cannot open a procedure file while procedures are executing. Thus, you can't invoke OpenProc from within a procedure. You can invoke it only from the command line or from a user menu definition (actually, you may get away with it in a macro, but it's not recommend).

### *See Also* {#see-also}
[Procedure Windows](/igorpro/programming/procedure-windows.md)

[Execute](/igorpro/commands/execute.md), [CloseProc](/igorpro/commands/closeproc.md)