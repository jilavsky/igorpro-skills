---
description: "The KillWindow operation kills or closes a specified window or subwindow without saving a recreation macro."
slug: /commands/killwindow
---

<div className="command-signature">

## <strong>KillWindow</strong>  [/Z] <em>winName</em> {#killwindow}

</div>

The KillWindow operation kills or closes a specified window or subwindow without saving a recreation macro.

### *Parameters* {#parameters}
*winName* is the name of an existing window or subwindow.

When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Does not generate an error if the specified window does not exist. |
|  | The /Z flag was added in Igor Pro 7.00. |

### *See Also* {#see-also}
[DoWindow](/igorpro/commands/dowindow.md)