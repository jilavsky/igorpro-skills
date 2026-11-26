---
description: "The RemoveFromTable operation removes the specified columns from the top table."
slug: /commands/removefromtable
---

<div className="command-signature">

## <strong>RemoveFromTable</strong>   [/W=<em>winName</em> ] <em>columnSpec</em> [,<em>columnSpec</em>]... {#removefromtable}

</div>

The RemoveFromTable operation removes the specified columns from the top table.

### *Parameters* {#parameters}
*columnSpecs*  are the same as for the Edit operation; usually they are just the names of waves.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Removes columns from the named table window or subwindow. When omitted, action will affect the active window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *See Also* {#see-also}
[Edit](/igorpro/commands/edit.md) about *columnSpecs*, and [AppendToTable](/igorpro/commands/appendtotable.md).