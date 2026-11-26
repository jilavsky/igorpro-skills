---
description: "The GetAxis operation determines the axis range and sets the variables V_min and V_max to the minimum and maximum values of the named axis."
slug: /commands/getaxis
---

<div className="command-signature">

## <strong>GetAxis</strong>  [/W=<em>winName</em> /Q] <em>axisName</em> {#getaxis}

</div>

The GetAxis operation determines the axis range and sets the variables V_min and V_max to the minimum and maximum values of the named axis.

### *Parameters* {#parameters}
*axisName*  is usually "left", "right", "top", or "bottom", though it may also be the name of a free axis such as "VertCrossing".

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | Prevents the values of V_flag, V_min and V_max from being printed in the history area. The results are still stored in the variables. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Retrieves axis info from the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
More precisely, GetAxis sets V_min according to the bottom of vertical axes or left of horizontal axes and V_max according to the top of vertical axes or right of horizontal axes. It also sets the variable V_flag to 0 if the specified axis is actually used in the graph, or to 1 if it is not.

Axis ranges and other graph properties are computed when the graph is redrawn. Since automatic screen updates are suppressed while a user-defined function is running, if the graph was recently created or modified, you must call DoUpdate to redraw the graph so you get accurate axis information.

### *See Also* {#see-also}
[AxisInfo](/igorpro/commands/axisinfo.md)