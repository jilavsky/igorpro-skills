---
description: "The SaveNotebook operation saves the named notebook. notebookName is either kwTopWin for the top notebook window, the name of a notebook window or a…"
slug: /commands/savenotebook
---

<div className="command-signature">

## <strong>SaveNotebook</strong>  [<em>flags</em> ] <em>notebookName</em>  [<em>as</em> <em>fileNameStr</em> ] {#savenotebook}

</div>

The SaveNotebook operation saves the named notebook.

### *Parameters* {#parameters}
*notebookName* is either kwTopWin for the top notebook window, the name of a notebook window or a host-child specification (an hcSpec) such as Panel0#nb0. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on host-child specifications.

If *notebookName* is an host-child specification, /S must be used and *saveType* must be 3 or higher.

The file to be written is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If Igor cannot determine the location of the file from *fileNameStr* and *pathName*, it displays a dialog allowing you to specify the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |  |
| --- | --- | --- |
| <span class="table-cell-nowrap">/ENCG = *textEncoding*</span> | Specifies text encoding in which the notebook is to be saved. |  |
|  | This flag was added in Igor Pro 7.00. |  |
|  | This is relevant for plain text notebooks only and is ignored for formatted notebooks because they can contain multiple text encodings. See [Plain Text File Text Encodings](/igorpro/igor-basics/text-encodings.md#plain-text-file-text-encodings) and [Formatted Text Notebook File Text Encodings](/igorpro/igor-basics/text-encodings.md#formatted-text-notebook-file-text-encodings) for details. |  |
|  | If omitted, the file is saved in its original text encoding. Normally you should omit /ENCG. Use it only if you have some reason to change the file's text encoding. |  |
|  | Passing 0 for *textEncoding* acts as if /ENCG were omitted. |  |
|  | See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for a list of accepted values for *textEncoding*. |  |
|  | This flag does not affect HTML export. Use /H instead. |  |
| <span class="table-cell-nowrap">/H = {*encodingName*, *writeParagraphProperties*, *writeCharacterProperties*, *PNGOrJPEG*, *quality*, *bitDepth* }</span> |  |  |
|  | This flag affects writing an HTML file. |  |
|  | *encodingName* | Sets the HTML file text encoding. The recommended value is "UTF-8". |
|  | *writeParagraphProperties* |  |
|  |  | Determines what paragraph properties SaveNotebook will write to the HTML file. This is a bitwise parameter with the bits defined as follows: |
|  |  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Write paragraph alignment.</td></tr><tr><td>Bit&nbsp;1:</td><td>Write first indent.</td></tr><tr><td>Bit&nbsp;2:</td><td>Write minimum line spacing.</td></tr><tr><td>Bit&nbsp;3:</td><td>Write space-before and space-after paragraph.</td></tr></tbody></table>
|  |  | All other bits are reserved for future use and should be set to zero. |
|  | *writeCharacterProperties* |  |
|  |  | Determines what character properties SaveNotebook will write to the HTML file. This is a bitwise parameter with the bits defined as follows: |
|  |  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Write font families.</td></tr><tr><td>Bit&nbsp;1:</td><td>Write font sizes.</td></tr><tr><td>Bit&nbsp;2:</td><td>Write font styles.</td></tr><tr><td>Bit&nbsp;3:</td><td>Write text colors.</td></tr><tr><td>Bit&nbsp;4:</td><td>Write text vertical offsets.</td></tr></tbody></table>
|  |  | All other bits are reserved for future use and should be set to zero. |
|  |  | If you set bit 2, SaveNotebook exports only the bold, underline, and italic styles because other character styles are not supported by HTML. |
|  | *PNGOrJPEG* | Determines whether SaveNotebook will write picture files as PNG or JPEG: |
|  |  |<table class="nested-table"><tbody><tr><td>0:</td><td>Write as PNG  (default).</td></tr><tr><td>1:</td><td>Write as JPEG.</td></tr><tr><td>2:</td><td>Write as JPEG.</td></tr></tbody></table>
|  |  | In Igor 7 and later, there is no difference between *PNGOrJPEG*=1 and *PNGOrJPEG*=2. |
|  |  | See below for details on HTML picture files. |
|  | *quality* | Specifies the degree of compression or image quality when writing pictures as JPEG files. Legal values are in the range 0.0 to 1.0. |
|  |  | In Igor 7 or later, the quality used is always .9 regardless of what you pass for this parameter. |
|  | *bitDepth* | Specifies the color depth when writing pictures as JPEG files. Legal values are 1, 8, 16, 24, and 32. |
|  |  | In Igor 7 or later, the bit depth used is always 32 regardless of what you pass for this parameter. |
| <span class="table-cell-nowrap">/I</span> | The save is interactive. A dialog is displayed. |  |
| <span class="table-cell-nowrap">/M = *messageStr*</span> | Specifies prompt message used in save dialog. |  |
| <span class="table-cell-nowrap">/O</span> | Overwrites existing file without asking permission. |  |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to store the file in. *pathName* is the name of an existing symbolic path. |  |
| <span class="table-cell-nowrap">/S = *saveType*</span> | *saveType* =1: | Normal save (default). |
|  | *saveType* =2: | Save-as. |
|  | *saveType* =3: | Save-a-copy. |
|  | *saveType* =4: | Export as RTF (Rich Text Format). |
|  | *saveType* =5: | Export as HTML (Hypertext Markup Language). |
|  | *saveType* =6: | Export as plain text. |
|  | *saveType* =7: | Export as formatted notebook. |
|  | *saveType* =8: | Export as plain text with line breaks. |

### *Details* {#details}
Interactive (/I) means that Igor displays the Save, Save as or Save a Copy dialog.

The save will be interactive under the following conditions:


-	You include the /I flag and the *saveType* is 2, 3, 4, 5, 6, 7 or 8.


-	*saveType* is 2, 3, 4, 5, 6, 7 or 8 and you do not specify the path or filename.

If the *saveType* is normal and the notebook has previously been saved to a file then the /I flag, the path and file name that you specify, if any, are ignored and the notebook is saved to its associated file without user intervention.

The full path to the saved file is stored in the string S_path. If the save was unsuccessful, S_path will be "".

If you use /P=*pathName* , note that it is the name of an Igor symbolic path, created via [NewPath](/igorpro/commands/newpath.md). It is not a file system path like "hd:Folder1:" or "C:\\\\Folder1\\\\". See [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths) for details.

*saveType*=8 applies to formatted notebooks only. It exports the notebook as plain text with line breaks added where text wraps in the formatted notebook. This feature was added in Igor Pro 8.00. Special characters such as pictures are skipped. If the notebook is plain text then *saveType*=8 acts like *saveType*=6.

### *Exporting as RTF* {#exporting-as-rtf}
For background information on writing RTF files, see [Import and Export Via Rich Text Format Files](/igorpro/igor-basics/notebooks.md#import-and-export-via-rich-text-format-files).

### *Exporting as HTML* {#exporting-as-html}
For background information on writing HTML files, see [Exporting a Notebook as HTML](/igorpro/igor-basics/notebooks.md#exporting-a-notebook-as-html).

You can pass "UTF-8" or "UTF-2" for the /H *encodingName* parameter. In virtually all cases, you should pass "UTF-8".

When creating an HTML file, Igor can write pictures using the PNG or JPEG graphics formats. PNG is recommended because it is lossless.

### *See Also* {#see-also}
[Notebooks](/igorpro/igor-basics/notebooks.md)

[Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.