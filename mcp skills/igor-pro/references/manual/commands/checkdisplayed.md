---
description: "The CheckDisplayed operation determines if named waves are displayed or otherwise used in a host window or subwindow."
slug: /commands/checkdisplayed
---

<div className="command-signature">

## <strong>CheckDisplayed</strong>  [/A/W=<em>winName</em> ] <em>waveName</em> [, <em>waveName</em> ]... {#checkdisplayed}

</div>

The CheckDisplayed operation determines if named waves are displayed or otherwise used in a host window or subwindow.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Checks all graphs, tables, page layout, panels, and Gizmo windows. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Checks only the named window. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
If neither /A nor /W are used, CheckDisplayed checks only the top graph, table, page layout, panel, or Gizmo window.

CheckDisplayed sets the variable V_flag on a bitwise basis according to which waves are displayed.

Waves that are not directly displayed in a window can still be used by it. For example, CheckDisplayed returns 1 for the following case: waves associated with hidden traces, color index waves, waves used to specify error bars, and waves used to draw polygons including in page layouts and control panels as well as graphs.

### *Example* {#example}

```igor
// Checks Graph0 to see if aWave, bWave, and cWave are displayed in it.
// Sets bit 0 of V_flag if aWave is displayed.
// Sets bit 1 of V_flag if bWave is displayed.
// Sets bit 2 of V_flag if cWave is displayed.
CheckDisplayed/W=Graph0 aWave,bWave,cWave
```

### *See Also* {#see-also}
[Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.