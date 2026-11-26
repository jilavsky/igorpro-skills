---
description: "The CloseProc operation closes a procedure window. You cannot call CloseProc on the main Procedure window."
slug: /commands/closeproc
---

<div className="command-signature overload">

## <strong>CloseProc</strong>   /NAME=<em>procNameStr</em>  [/P=<em>PathName</em> ] [/COMP=[<em>compile</em> ] [/D=[<em>delete</em> ]] [/SAVE[=<em>savePathStr</em> ]] {#closeproc}

</div>
<div className="command-signature">

## <strong>CloseProc</strong>   /FILE=<em>procFileStr</em>  [/P=<em>PathName</em> ] [/COMP=[<em>compile</em> ] [/D=[<em>delete</em> ]] [/SAVE[=<em>savePathStr</em> ]] {#closeproc}

</div>

The CloseProc operation closes a procedure window. You cannot call CloseProc on the main Procedure window.

CloseProc provides a way to programmatically create and alter procedure files. You might do this in order to make a user-defined menu-bar menu with contents that change.

:::note
CloseProc alters procedure windows so it cannot be called while functions or macros are running. If you want to call it from a function or macro, use Execute/P.
:::

:::caution
If you close a procedure window that has no source file or without specifying a destination file, the window contents will be permanently lost.
:::

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/COMP[ = *compile* ]</span> |  |
|  | Specifies whether procedures should be compiled after closing the procedure window. |
|  |<table class="nested-table"><tbody><tr><td>*compile*&nbsp;=1:</td><td>Compiles procedures (same as /COMP only).</td></tr><tr><td>*compile*&nbsp;=0:</td><td>Leaves procedures in an uncompiled state.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/D[ = *delete* ]</span> | Specifies whether the procedure file should be deleted after closing its procedure window. |
|  |<table class="nested-table"><tbody><tr><td>*delete*&nbsp;=0:</td><td>Leaves any associated file unaffected.</td></tr><tr><td>*delete*&nbsp;=1:</td><td>Deletes procedure file (same as /D only).</td></tr></tbody></table>
|  | <div><Admonition type="caution"><p>You cannot recover any file deleted using */D = 1*</p></Admonition></div> |
| <span class="table-cell-nowrap">/FILE = *fileNameStr*</span> |  |
|  | Identifies the procedure window to close using the file name and path to the file given by *fileNameStr*. The string can be just the file name if /P is used to specify a symbolic path name of the enclosing folder. It can be a partial path if /P points to a folder enclosing the start of the partial path. It can also be a full path the file. |
| <span class="table-cell-nowrap">/NAME = *procNameStr*</span> |  |
|  | Identifies the procedure window to close with the string expression *procNameStr*. This is the same text that appears in the window title. If the procedure window is associated with a file, it will be the file name and extension. |
|  | To close a procedure file that is part of an independent module, you must include the independent module name in *procNameStr* . For example: |
|  | <code class="igor">CloseProc /NAME="GraphBrowser.ipf [WM_GrfBrowser]"</code> |
|  | Note that there is a space after the file name followed by the independent module name in brackets. |
| <span class="table-cell-nowrap">/P = *pathname*</span> | Specifies the folder to look in for the file specified by /FILE. *pathName* is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/SAVE[ = *savePathStr* ]</span> |  |
|  | Saves the procedure before closing the window. If the flag is used with no argument, it saves any changes to the procedure window to its source file before closing it. If *savePathStr* is present, it must be a full path naming a file in which to save the procedure window contents. The /P flag is not used with *savePathStr* so it must be a full path. |

### *Details* {#details}
CloseProc cannot be called from a macro or function. Call it from the command line or via Execute/P (see [Operation Queue](/igorpro/advanced-topics.md#operation-queue)).

Specify which window to close using either the /NAME or /FILE flag. You must use one or the other. Usually you would use /NAME, as it is usually more convenient. If by some chance two procedures have the same name, /FILE can be used to distinguish between them.

You cannot call CloseProc on a nonmain procedure window that someone has had the bad taste to call "Procedure".

### *See Also* {#see-also}
[Procedure Windows](/igorpro/programming/procedure-windows.md)

The [Execute](/igorpro/commands/execute.md) operation.