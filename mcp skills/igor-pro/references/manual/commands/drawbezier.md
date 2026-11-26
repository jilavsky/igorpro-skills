---
description: "The DrawBezier operation draws a Bezier curve with first point of the curve positioned at xOrg and yOrg."
slug: /commands/drawbezier
---

<div className="command-signature overload">

## <strong>DrawBezier</strong>  [/W=<em>winName</em> /ABS] <em>xOrg</em>, <em>yOrg</em>, <em>hScaling</em>, <em>vScaling</em>, <em>xWaveName</em>, <em>yWaveName</em> {#drawbezier}

</div>
<div className="command-signature overload">

## <strong>DrawBezier</strong>  [/W=<em>winName</em> /ABS] <em>xorg</em>, <em>yorg</em>, <em>hScaling</em>, <em>vScaling</em>, {<em>x0</em>, <em>y0</em>, <em>x1</em>, <em>y1</em> ...} {#drawbezier}

</div>
<div className="command-signature">

## <strong>DrawBezier/A</strong>  [/W=<em>winName</em> ] {<em>xn</em>, <em>yn</em>, <em>xn</em>+, <em>yn</em>+ ...} {#drawbezier-a}

</div>

The DrawBezier operation draws a Bezier curve with first point of the curve positioned at *xOrg* and *yOrg*.

### *Parameters* {#parameters}

(*xOrg*, *yOrg*) defines the starting point for the Bezier curve in the currently active coordinate system.

*hScaling* and *vScaling* set the horizontal and vertical scale factors about the origin, with 1 meaning 100%.

The *xWaveName*, *yWaveName* version of DrawBezier gets data from the named X and Y waves. This connection is maintained so that any changes to either wave will result in updates to the Bezier curve.

To use the version of DrawBezier that takes a literal list of vertices, you place as many vertices as you like on the first line and then use as many /A versions as necessary to define all the vertices.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Appends the given vertices to the currently open Bezier (freshly drawn or current selection). |
| <span class="table-cell-nowrap">/ABS</span> | Suppresses the default subtraction of the first point from the rest of the data. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Draws to the named window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line.<br>When identifying a subwindow with *winName*, see Subwindow Syntax for details on forming the window hierarchy. |

### *Details* {#details}

Data waves defining Bezier curves must have 1+3\**n*  data points. Every third data point is an anchor point and lies on the curve; intervening points are control points that define the direction of the curve relative to the adjacent anchor point.

Normally, you should create and edit a Bezier curve using drawing tools, and not calculate values. See [Polygon Tool](/igorpro/graphing/drawing.md#polygon-tool) and [Editing a Bezier Curve](/igorpro/graphing/drawing.md#editing-a-bezier-curve) for instructions.

You can include the /ABS flag to suppress the default subtraction of the first point.

To change just the origin and scale without respecifying the data use:

```igor
DrawBezier xOrg, yOrg, hScaling, vScaling,{}
```

It is possible to separate a Bezier curve into segments by adding coordinate pairs that are NaN. For details, see [Segmented Bezier Curves](/igorpro/graphing/drawing.md#segmented-bezier-curves).

### *Example* {#example}

For an example using Bezier curves, see Segmented Bezier Curves.

### *See Also* {#see-also}

[Drawing](/igorpro/graphing/drawing.md)

[SetDrawEnv](/igorpro/commands/setdrawenv.md), [SetDrawLayer](/igorpro/commands/setdrawlayer.md)

[DrawArc](/igorpro/commands/drawarc.md), [DrawPoly](/igorpro/commands/drawpoly.md), [DrawAction](/igorpro/commands/drawaction.md), [BezierToPolygon](/igorpro/commands/beziertopolygon.md)