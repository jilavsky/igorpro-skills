---
description: "The DrawPoly operation draws a polygon in the target graph, layout or control panel."
slug: /commands/drawpoly
---

<div className="command-signature overload">

## <strong>DrawPoly</strong>  [/W=<em>winName</em> /ABS] <em>xorg</em>, <em>yorg</em>, <em>hScaling</em>, <em>vScaling</em>, <em>xWaveName</em>, <em>yWaveName</em> {#drawpoly}

</div>
<div className="command-signature overload">

## <strong>DrawPoly</strong>  [/W=<em>winName</em> /ABS] <em>xorg</em>, <em>yorg</em>, <em>hScaling</em>, <em>vScaling</em>, {<em>x0</em>, <em>y0</em>, <em>x1</em>, <em>y1</em> ...} {#drawpoly}

</div>
<div className="command-signature">

## <strong>DrawPoly</strong> [/W=<em>winName</em> ]/A {xn, yn, xn+, yn+ ...} {#drawpoly}

</div>

The DrawPoly operation  draws a polygon in the target graph, layout or control panel.

### *Parameters* {#parameters}

(*xorg*, *yorg*) defines the starting point for the polygon in the currently active coordinate system.

*hScaling* and *vScaling* set the horizontal and vertical scale factors, with 1 meaning 100%.

The *xWaveName*, *yWaveName* version of DrawPoly gets data from those X and Y waves. This connection is maintained so that any changes to either wave will result in updates to the polygon. 

The DrawPoly operation is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

To use the version of DrawPoly that takes a literal list of vertices, you place as many vertices as you like on the first line and then use as many /A versions as necessary to define all the vertices.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Appends the given vertices to the currently open polygon (freshly drawn or current selection). |
| <span class="table-cell-nowrap">/ABS</span> | Suppresses the default subtraction of the first point from the rest of the data. |
| <span class="table-cell-nowrap">/W = winName</span> | Draws to the named window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line.<br>When identifying a subwindow with winName, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}

Because *xorg* and *yorg* define the location of the starting vertex of the poly, adding or subtracting a constant from the vertices will have no effect. The first XY pair in the {*x<sub>0</sub>*, *y<sub>0</sub>*, *x<sub>1</sub>*, *y<sub>1</sub>* ...} vertex list will appear at (*xorg*, *yorg*) regardless of the value of *x<sub>0</sub>* and *y<sub>0</sub>*. *x<sub>0</sub>* and *y<sub>0</sub>* merely serve to set a reference point for the list of vertices. Subsequent vertices are relative to (*x<sub>0</sub>*, *y<sub>0</sub>*).

To keep your mental health intact, we recommend that you specify (*x<sub>0</sub>*, *y<sub>0</sub>*) as (0,0) so that all the following vertices are offsets from that origin. Then (*xorg*, *yorg*) sets the position of the polygon and all of the vertices in the list are relative to that origin.

An alternate method is to use the same values for (*x<sub>0</sub>*, *y<sub>0</sub>*) as for (*xorg*, *yorg*) if you consider the vertices to be "absolute" coordinates.

You can include the /ABS flag to suppress the subtraction of the first point.

To change just the origin and scale of the currently open polygon — without having to respecify the data use:

```igor
DrawPoly xorg, yorg, hScaling, vScaling,{}
```

The coordinate system as well as the polygon's thickness, color, dash pattern and other properties are determined by the current drawing environment. The polygon is drawn in the current draw layer for the window, as determined by SetDrawLayer.

It is possible to separate a polygon into segments by adding coordinate pairs that are NaN. For details, see [Segmented Polygons](/igorpro/graphing/drawing.md#segmented-polygons).

### *Examples* {#examples}

Here are some commands to draw some small triangles using absolute drawing coordinates (see SetDrawEnv).

```igor
Display	// make a new empty graph

// Draw one triangle, starting at 50,50 at 100% scaling
SetDrawEnv xcoord= abs,ycoord= abs
DrawPoly 50,50,1,1, {0,0,10,10,-10,10,0,0}

// Draw second triangle below and to the right, same size and shape
SetDrawEnv xcoord= abs,ycoord= abs
DrawPoly 100,100,1,1, {0,0,10,10,-10,10,0,0}
```

For another example using polygons, see [Segmented Polygons](/igorpro/graphing/drawing.md#segmented-polygons).

### *See Also* {#see-also}

[DrawPoly and DrawBezier Operations](/igorpro/graphing/drawing.md#drawpoly-and-drawbezier-operations)

[SetDrawEnv](/igorpro/commands/setdrawenv.md), [SetDrawLayer](/igorpro/commands/setdrawlayer.md), [DrawBezier](/igorpro/commands/drawbezier.md), [DrawAction](/igorpro/commands/drawaction.md), [PolygonOp](/igorpro/commands/polygonop.md), [BezierToPolygon](/igorpro/commands/beziertopolygon.md)