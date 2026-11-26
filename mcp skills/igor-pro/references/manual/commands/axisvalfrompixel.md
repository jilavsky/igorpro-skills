---
description: "The AxisValFromPixel function returns an axis value corresponding to the local graph pixel coordinate in the graph window or subwindow."
slug: /commands/axisvalfrompixel
---

<div className="command-signature">

## <strong>AxisValFromPixel</strong> (<em>graphNameStr</em>, <em>axNameStr</em>, <em>pixel</em>) {#axisvalfrompixel}

</div>

The AxisValFromPixel function returns an axis value corresponding to the local graph pixel coordinate in the graph window or subwindow.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph window.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

If the specified axis is not found and if the name is "left" or "bottom" then the first vertical or horizontal axis will be used. Sources for *pixel* value may be the [GetWindow](/igorpro/commands/getwindow.md) operation or a user window hook with the mousemoved and mousedown event messages (see the [SetWindow](/igorpro/commands/setwindow.md) operation).

If *graphNameStr* references a subwindow, *pixel* is relative to top left corner of base window, not the subwindow.

Axis ranges and other graph properties are computed when the graph is redrawn. Since automatic screen updates are suppressed while a user-defined function is running, if the graph was recently created or modified, you must call DoUpdate to redraw the graph so you get accurate axis information.

### *See Also* {#see-also}
[PixelFromAxisVal](/igorpro/commands/pixelfromaxisval.md), [TraceFromPixel](/igorpro/commands/tracefrompixel.md)