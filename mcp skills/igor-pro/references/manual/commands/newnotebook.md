---
description: "The NewNotebook operation creates a new notebook document. the optional titleStr is a string containing the title of the notebook window."
slug: /commands/newnotebook
---

<div className="command-signature">

## <strong>NewNotebook</strong>  [<em>flags</em> ] [<em>as</em> <em>titleStr</em> ] {#newnotebook}

</div>

The NewNotebook operation creates a new notebook document.

### *Parameters* {#parameters}
the optional *titleStr* is a string containing the title of the notebook window.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/FG = (*gLeft*, *gTop*, *gRight*, *gBottom* )</span> |  |
|  | Specifies the frame guide to which the outer frame of the subwindow is attached inside the host window. |
|  | The standard frame guide names are FL, FR, FT, and FB for the left, right, top, and bottom frame guides, respectively, or user-defined guide names as defined by the host. Use * to specify a default guide name. |
|  | Guides may override the numeric positioning set by /W. |
| <span class="table-cell-nowrap">/HOST = *hcSpec*</span> | Embeds the new notebook in the host window or subwindow specified by *hcSpec*. The host window or subwindow must be a control panel. Graphs and page layouts are not supported as hosts for notebook subwindows. |
|  | When identifying a subwindow with *hcSpec*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
|  | See [Notebooks as Subwindows in Control Panels](/igorpro/graphing/making-figures/subwindows.md#notebooks-as-subwindows-in-control-panels) for more information. |
| <span class="table-cell-nowrap">/ENCG = *textEncoding*</span> | *textEncoding* specifies the text encoding for the new notebook. This determines the text encoding used for later saving the notebook to a file. |
|  | See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for a list of accepted values for *textEncoding*. |
|  | This flag was added in Igor Pro 7.00. |
|  | This flag is relevant for plain text notebooks only and has no effect for formatted notebooks because formatted text notebooks can contain multiple text encodings. See [Plain Text File Text Encodings](/igorpro/igor-basics/text-encodings.md#plain-text-file-text-encodings) and [Formatted Text Notebook File Text Encodings](/igorpro/igor-basics/text-encodings.md#formatted-text-notebook-file-text-encodings) for details. |
|  | If you omit /ENCG or pass 0 (unknown) for *textEncoding* , the notebook's text encoding is determined by the default text encoding - see [The Default Text Encoding](/igorpro/igor-basics/text-encodings.md#the-default-text-encoding) for details. |
|  | For most purposes, UTF-8 (*textEncoding* =1) is recommended. Other values are available for compatibility with software that requires a specific text encoding. This includes Igor Pro 6 which uses MacRoman (*textEncoding* =2), Windows-1252 (*textEncoding* =3) or Shift-JIS (*textEncoding* =4) depending on the operating system and localization. |
|  | This flag has an optional form that allows you to control whether the byte order mark is written when the notebook is later saved to disk. It applies to Unicode text encodings also. The form is: |
|  | <code class="igor">/ENCG = {textEncoding, writeBOM}</code> |
|  | If you use the simpler form or omit /ENCG entirely, the notebook's writeBOM property defaults to 1. |
|  | See [Byte Order Marks](/igorpro/igor-basics/text-encodings.md#byte-order-marks) for background information. |
| /F=*format* |<table class="nested-table"><tbody><tr><td>*format*&nbsp;=0:</td><td>Plain text.</td></tr><tr><td>*format*&nbsp;=1:</td><td>Formatted text.</td></tr><tr><td>*format*&nbsp;=-1:</td><td>Displays a dialog asking in which the user can choose plain text or formatted text (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/K = *k*</span> | Specifies window behavior when the user attempts to close it. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr><tr><td>*k*&nbsp;=3:</td><td>Hides the window.</td></tr><tr><td>*k*&nbsp;=4:</td><td>Kills with no dialog and is not saved with the experiment.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/N = *winName*</span> | Sets the notebook's window name. |
| <span class="table-cell-nowrap">/OPTS = *options*</span> | Sets special options. *options* is a bitwise parameter interpreted as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Hide the vertical scroll bar.</td></tr><tr><td>Bit&nbsp;1:</td><td>Hide the horizontal scroll bar.</td></tr><tr><td>Bit&nbsp;2:</td><td>Set the write-protect icon initially to on.</td></tr><tr><td>Bit&nbsp;3:</td><td>Sets the changeableByCommandOnly notebook property. When set, the user cannot make any modifications.</td></tr></tbody></table>
|  | All other bits are reserved for future use and are currently ignored. Pass zero for all reserved bits. |
|  | If /OPTS is omitted, all bits default to zero. |
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about setting bits. |
| /V=*visible* |<table class="nested-table"><tbody><tr><td>*visible*&nbsp;=0:</td><td>Invisible.</td></tr><tr><td>*visible*&nbsp;=1:</td><td>Visible (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom*)</span> |  |
|  | Sets window location. Coordinates are in points for normal notebook windows. |
|  | When used with the /HOST flag, the specified location coordinates can have one of two possible meanings: |
|  |<table class="nested-table"><tbody><tr><td>1.</td><td>When all values are less than 1, coordinates are assumed to be fractional relative to the host frame size.</td></tr><tr><td>2.</td><td>When any value is greater than 1, coordinates are taken to be fixed locations measured in points, or [control panel units](/igorpro/user-interface/controls.md#control-panel-units) for control panel hosts, relative to the top left corner of the host frame.</td></tr></tbody></table>

### *Details* {#details}
A notebook has a file name, a window name, and a window title. In the simplest case these will all be the same.

The file name is the name by which the operating system identifies the notebook once it is saved to disk. When you initially create a notebook, it is not associated with any file. However it still has a file name. This is the name that will be used when the file is saved to disk.

The window name is the name by which Igor identifies the window and therefore the name you specify in operations that act on the notebook.

The window title is what appears in the window's title bar. If you omit the title, NewNotebook uses a default title which is the same as the window name.

If you specify the window name and the notebook format and omit the window title, this is the simplest case. NewNotebook creates the document with no user interaction. The file name, window name and window title will all be the same. For example:


```igor
NewNotebook/N=Notebook1/F=0
```

If you omit the window name NewNotebook chooses a default name (e.g., Notebook0) and presents the standard New Notebook dialog.

If you omit the format or specify a format of -1 (either plain or formatted text), NewNotebook presents the standard New Notebook dialog. For example::


```igor
NewNotebook/N=Notebook1	// no format specified
```

### *See Also* {#see-also}
[Notebook](/igorpro/commands/notebook.md), [NewNotebook](/igorpro/commands/newnotebook.md), [Notebooks](/igorpro/igor-basics/notebooks.md)

[Notebooks as Subwindows in Control Panels](/igorpro/graphing/making-figures/subwindows.md#notebooks-as-subwindows-in-control-panels)