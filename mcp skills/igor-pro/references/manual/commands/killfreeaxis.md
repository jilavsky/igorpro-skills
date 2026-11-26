---
description: "The KillFreeAxis operation removes a free axis specified by axisName from a graph window or subwindow."
slug: /commands/killfreeaxis
---

<div className="command-signature">

## <strong>KillFreeAxis</strong>  [/W=<em>winName</em> ] <em>axisName</em> {#killfreeaxis}

</div>

The KillFreeAxis operation removes a free axis specified by *axisName* from a graph window or subwindow.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Kills the free axis in the named graph window or subwindow. If /W is omitted, it acts on the top graph window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
Only an axis created by [NewFreeAxis](/igorpro/commands/newfreeaxis.md) can be killed and only if no traces or images are attached to the axis.

### *See Also* {#see-also}
[NewFreeAxis](/igorpro/commands/newfreeaxis.md)