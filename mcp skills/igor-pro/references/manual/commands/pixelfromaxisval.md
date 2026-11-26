---
description: "The PixelFromAxisVal function returns the local graph pixel coordinate corresponding to the axis value in the graph window or subwindow."
slug: /commands/pixelfromaxisval
---

<div className="command-signature">

## <strong>PixelFromAxisVal</strong> (<em>graphNameStr</em>, <em>axNameStr</em>, <em>val</em>) {#pixelfromaxisval}

</div>

The PixelFromAxisVal function returns the local graph pixel coordinate corresponding to the axis value in the graph window or subwindow.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph window.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

If the specified axis is not found and if the name is "left" or "bottom" then the first vertical or horizontal axis will be used.

If *graphNameStr* references a subwindow, the returned pixel value is relative to top left corner of base window, not the subwindow.

Axis ranges and other graph properties are computed when the graph is redrawn. Since automatic screen updates are suppressed while a user-defined function is running, if the graph was recently created or modified, you must call DoUpdate to redraw the graph so you get accurate axis information.

### *See Also* {#see-also}
[AxisValFromPixel](/igorpro/commands/axisvalfrompixel.md), [TraceFromPixel](/igorpro/commands/tracefrompixel.md)