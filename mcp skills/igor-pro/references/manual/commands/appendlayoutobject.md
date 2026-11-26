---
description: "The AppendLayoutObject operation appends a single object to the top layout or to the layout specified via the /W flag."
slug: /commands/appendlayoutobject
---

<div className="command-signature">

## <strong>AppendLayoutObject</strong>  [<em>flags</em>] <em>objectType</em>  <em>objectName</em> {#appendlayoutobject}

</div>

The AppendLayoutObject operation appends a single object to the top layout or to the layout specified via the /W flag. It targets the active page or the page specified by the /PAGE flag.

Unlike the AppendToLayout operation, AppendLayoutObject can be used in user-defined functions. Therefore, AppendLayoutObject should be used in new programming instead of AppendToLayout.

### *Parameters* {#parameters}
*objectType* identifies the type of object to be appended. It is one of the following keywords: `graph`, `table`, `picture`, `gizmo`.

*objectName*  is the name of the graph, table, picture or Gizmo window to be appended.

Use a space between *objectType* and *objectName*. A comma is not allowed.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D = *fidelity*</span> | *fidelity*  is 0 to make the object low fidelity or 1 (default) to make it high fidelity. This affects drawing on the screen only, not exporting or printing. Low fidelity is somewhat faster but less accurate. It should be used only for graphs that take a very long time to draw. |
| /F=*frame* |<table class="nested-table"><tbody><tr><td>*frame*&nbsp;=0:</td><td>No frame.</td></tr><tr><td>*frame*&nbsp;=1:</td><td>Single frame (default).</td></tr><tr><td>*frame*&nbsp;=2:</td><td>Double frame.</td></tr><tr><td>*frame*&nbsp;=3:</td><td>Triple frame.</td></tr><tr><td>*frame*&nbsp;=4:</td><td>Shadow frame.</td></tr></tbody></table>
| /T=*trans* |<table class="nested-table"><tbody><tr><td>*trans*&nbsp;=0:</td><td>Opaque (default).</td></tr><tr><td>*trans*&nbsp;=1:</td><td>Transparent.</td></tr></tbody></table>
|  | For this to be effective, the object itself must also be transparent. Annotations have their own transparent/opaque settings. Graphs are transparent only if their backgrounds are white. PICTs may have been created transparent or opaque, and Igor cannot make an opaque PICT transparent. |
| <span class="table-cell-nowrap">/PAGE = *page*</span> | Appends the object to the specified page. |
|  | Page numbers start from 1. To target to the active page, omit /PAGE or use *page*=0. |
|  | The /PAGE flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/R = (*l*, *t*, *r*, *b* )</span> | Sets the size and position of the object. If omitted, the object is placed with a default size and position. *l*, *t*, *r*, and *b* are the left, top, right, and bottom coordinates of the object respectively. Coordinates are expressed in units of points, relative to the top/left corner of the paper. |
| <span class="table-cell-nowrap">/W = *winName*</span> | *winName* is the name of the page layout window to which the object is to be appended. If /W is omitted or if *winName* is $"", the top page layout is used. |

### *See Also* {#see-also}
[NewLayout](/igorpro/commands/newlayout.md), [ModifyLayout](/igorpro/commands/modifylayout.md), [RemoveLayoutObjects](/igorpro/commands/removelayoutobjects.md), [Textbox](/igorpro/commands/textbox.md), [Legend](/igorpro/commands/legend.md)