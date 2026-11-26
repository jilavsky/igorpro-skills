---
description: "The DrawArc operation draws a circular counterclockwise arc with center at xOrg and yOrg."
slug: /commands/drawarc
---

<div className="command-signature">

## <strong>DrawArc</strong>  [/W=<em>winName</em> /X/Y/ORIG] <em>xOrg</em>, <em>yOrg</em>, <em>arcRadius</em>, <em>startAngle</em>, <em>stopAngle</em> {#drawarc}

</div>

The DrawArc operation draws a circular counterclockwise arc with center at *xOrg* and *yOrg*.

### *Parameters* {#parameters}
(*xOrg*, *yOrg*) defines the center point for the arc in the currently active coordinate system.

Angles are measured in degrees increasing in a counterclockwise direction. The *startAngle* specifies the starting angle for the arc and *stopAngle* specifies the end. If *stopAngle* is equal to *startAngle*, 360 degrees is added to *stopAngle*. Thus a circle can be drawn using *startAngle* = *stopAngle*.

The *arcRadius*  is the radial distance measured in points from (*xOrg*, *yOrg* ), unless /X or /Y are specified.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ORIG</span> | Draws lines from the arc start and end to the origin at (*xOrg*, *yOrg* ). Any arrows continue to be drawn at the arc start and stop endpoints on the arc's curve. /ORIG was added for Igor 10. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Draws to the named window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/X</span> | Measures *arcRadius* using the current X-coordinate system. If /Y is also used, the arc may be elliptical. |
| <span class="table-cell-nowrap">/Y</span> | Measures *arcRadius* using the current Y-coordinate system. If /X is also used, the arc may be elliptical. |

### *Details* {#details}
Arcs honor the current dash pattern and arrowhead setting in the same way as polygons and Beziers. In fact, arcs are implemented using Bezier curves.

Normally, you would create arcs programmatically. If you need to sketch an arc-like object, you should probably use a Bezier curve because it is more flexible and easier to adjust. However, there is one handy feature of arcs that make them useful for manual drawing: the origin can be in any of the supported coordinate systems and the radius is in points.

However, there is one handy feature of arcs that make them useful for manual drawing: the origin can be in any of the supported coordinate systems and the radius can be specified in points.

To draw an arc interactively, see [Arcs and Circles](/igorpro/graphing/drawing.md#arcs-and-circles) for instructions.

### *See Also* {#see-also}
[Drawing](/igorpro/graphing/drawing.md)

[SetDrawEnv](/igorpro/commands/setdrawenv.md), [SetDrawLayer](/igorpro/commands/setdrawlayer.md)

[DrawBezier](/igorpro/commands/drawbezier.md), [DrawOval](/igorpro/commands/drawoval.md), [DrawAction](/igorpro/commands/drawaction.md)