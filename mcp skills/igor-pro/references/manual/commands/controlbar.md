---
description: "The ControlBar operation sets the size (height or width) and location (top/left/bottom/right) of a control bar in a graph."
slug: /commands/controlbar
---

<div className="command-signature">

## <strong>ControlBar</strong>  [ /EXP=<em>e</em> /L/R/B/T/W=<em>graphName</em> ] <em>barSize</em> {#controlbar}

</div>

The ControlBar operation sets the size (height or width) and location (top/left/bottom/right) of a control bar in a graph.

For graphs with no controls, you do not need to use this operation.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/EXP = *e*</span> | Sets the expansion of the control bar area. |
|  | See the [NewPanel](/igorpro/commands/newpanel.md) operation /EXP flag for details. |
|  | The /EXP flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/L/R/B/T</span> | Designates whether to change the size of a control bar on the left, right, bottom, or top (default) edge of the graph, respectively, for the control bar location. |
| <span class="table-cell-nowrap">/W = *graphName*</span> | Specifies the name of a particular graph containing a control bar. |

### *Parameters* {#parameters}
*barSize*  is in pixels or points, depending on the screen resolution. See [Control Panel Resolution on Windows](/igorpro/user-interface/platform-related-issues.md#control-panel-resolution-on-windows) for details.

Setting *barSize*  to zero removes the specified control bar.

### *Details* {#details}
The control bar is an area normally at the top of graphs reserved for controls such as buttons, checkboxes and pop-up menus. A line is drawn between this area and the graph area. It may be assigned a separate background color by pressing Ctrl and clicking in the area, or by right-clicking it, or with the ModifyGraph operation. You cannot use draw tools in this area.

Control bars can also be added to the left, right, and bottom edges of a graph by specifying /L, /R, and /B flags. These control bars lack the line between the bar and the graph area.

Use `ControlInfo kwControlBar` to get the current height of the top control bar in `V_height`. Same for `kwControlBarBottom`.

Use `ControlInfo kwControlBarLeft` to get the current width of the left control bar in `V_width`. Same for `kwControlBarRight`.

### *Recommendations* ### {#recommendations}
Controls placed in control bars do not reposition themselves when a graph is resized. This is often not a problem when the top or left control bars are used, but is definitely a problem when using the right or bottom control bars, in which case a fixed graph size may be useful.

Instead of using `ControlBar` alone, it is recommended to insert a panel subwindow into the graph where desired and then place controls within the panel subwindow, because controls will maintain their positions within the panel subwindow with the host graph is resized.

### *Examples* {#examples}

```igor
Display myData
ControlBar 35			// 35 pixels high
Button button0,pos={56,8},size={90,20},title="My Button"
```

### *See Also* {#see-also}
[Controls in Graphs](/igorpro/user-interface/controls.md#controls-in-graphs), [ControlInfo](/igorpro/commands/controlinfo.md)