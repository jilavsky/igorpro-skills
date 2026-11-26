---
description: "The NewLayout operation creates a page layout. Unlike the Layout operation, NewLayout can be used in user-defined functions."
slug: /commands/newlayout
---

<div className="command-signature">

## <strong>NewLayout</strong>  [=(<em>r</em>,<em>g</em>,<em>b</em>[,<em>a</em>]) /C=<em>color</em> /HIDE=<em>h</em> /K=<em>k</em> /N=<em>name</em> /P=<em>orientation</em> /W=(<em>left</em>,<em>top</em>,<em>right</em>,<em>bottom</em>)] [<em>as</em> <em>titleStr</em> ] {#newlayout}

</div>

The NewLayout operation creates a page layout.

Unlike the Layout operation, NewLayout can be used in user-defined functions. Therefore, NewLayout should be used in new programming instead of Layout.

NewLayout just creates the layout window. Use [AppendLayoutObject](/igorpro/commands/appendlayoutobject.md) to add objects to the window.

### *Parameters* {#parameters}
The optional *titleStr* parameter is a string expression containing the layout's title. If not specified, Igor will provide one which identifies the objects displayed in the graph.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B = (*r,g,b*[,*a*])</span> | Specifies the background color for the layout. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque white. |
| <span class="table-cell-nowrap">/C = *colorOnScreen*</span> |  |
|  | Obsolete. In ancient times, this flag switched the screen display of the layout between black and white and color. It is still accepted but has no effect. |
| <span class="table-cell-nowrap">/HIDE = *h*</span> | Hides (*h* = 1) or shows (*h* = 0, default) the window. |
| <span class="table-cell-nowrap">/K = *k*</span> | Specifies window behavior when the user attempts to close it. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr><tr><td>*k*&nbsp;=3:</td><td>Hides the window.</td></tr><tr><td>*k*&nbsp;=4:</td><td>Kills with no dialog and is not saved with the experiment.</td></tr></tbody></table>
|  | If you use /K=2 or /K=3, you can still kill the window using the [KillWindow](/igorpro/commands/killwindow.md) operation. |
| <span class="table-cell-nowrap">/N = *name*</span> | Requests that the layout have this name, if it is not in use. If it is in use, then *name*0, *name*1, etc are tried until an unused window name is found. In a function or macro, S_name is set to the chosen layout name. |
|  | If /N is not used, a name of the form "Layout*n* ", where *n* is some integer, is assigned. In a function or macro, the assigned name is stored in the S_name string. This is the name you can use to refer to the page layout window from a procedure. Use the [RenameWindow](/igorpro/commands/renamewindow.md) operation to rename the window. |
| <span class="table-cell-nowrap">/P = *orientation*</span> | Sets the orientation of the page in the layout to either Portrait or Landscape (e.g., `Layout/P=Landscape`). See ***Details*** below. |
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom*)</span> |  |
|  | Gives the layout window a specific location and size on the screen. Coordinates for /W are in points. |

### *Details* {#details}
When you create a new layout window, if preferences are enabled, the page size is determined by the preferred page size as set via the Capture Layout Prefs dialog. If preferences are disabled, as is usually the case when executing a procedure, the page is set to the factory default size.

### *See Also* {#see-also}
[AppendLayoutObject](/igorpro/commands/appendlayoutobject.md), [RemoveLayoutObjects](/igorpro/commands/removelayoutobjects.md), [ModifyLayout](/igorpro/commands/modifylayout.md)