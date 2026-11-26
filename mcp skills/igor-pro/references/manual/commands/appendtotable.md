---
description: "The AppendToTable operation appends the specified columns to the top table."
slug: /commands/appendtotable
---

<div className="command-signature">

## <strong>AppendToTable</strong>   [/W=<em>winName</em> ] <em>columnSpec</em> [, <em>columnSpec</em> ]... {#appendtotable}

</div>

The AppendToTable operation appends the specified columns to the top table.  *columnSpecs*  are the same as for the [Edit](/igorpro/commands/edit.md) operation; usually they are just the names of waves.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Appends columns to the named table window or subwindow. When omitted, action will affect the active window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *See Also* {#see-also}
[Edit](/igorpro/commands/edit.md) about *columnSpecs*, and [RemoveFromTable](/igorpro/commands/removefromtable.md).