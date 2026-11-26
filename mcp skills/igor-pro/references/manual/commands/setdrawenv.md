---
description: "The SetDrawEnv operation sets properties of the drawing environment. If one or more draw objects are selected in the top window then the SetDrawEnv command…"
slug: /commands/setdrawenv
---

<div className="command-signature">

## <strong>SetDrawEnv</strong>  [/W=<em>winName</em> ]  <em>keyword</em>  [=<em>value</em> ][, <em>keyword</em>  [=<em>value</em> ]]... {#setdrawenv}

</div>

The SetDrawEnv operation sets properties of the drawing environment.

If one or more draw objects are selected in the top window then the SetDrawEnv command will apply only to those objects.

If no objects are selected and if the keyword save is not used then the command applies only to the next object drawn.

If no objects are selected and if the keyword "save" is used then the command sets the environment for all following objects.

Each draw layer has its own draw environment settings.

### *Parameters* {#parameters}
SetDrawEnv can accept multiple *keyword* =*value* parameters on one line.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">arrow = *arr*</span> | Specifies the arrow head position on lines. |
|  |<table class="nested-table"><tbody><tr><td>*arr*&nbsp;=0:</td><td>No arrowhead (default).</td></tr><tr><td>*arr*&nbsp;=1:</td><td>Arrowhead at end.</td></tr><tr><td>*arr*&nbsp;=2:</td><td>Arrowhead at start.</td></tr><tr><td>*arr*&nbsp;=3:</td><td>Arrowhead at start and end.</td></tr></tbody></table>
| <span class="table-cell-nowrap">arrowfat = *afat*</span> | Ratio of arrowhead width to length, default is 0.5. |
| <span class="table-cell-nowrap">arrowlen = *alen*</span> | Length of arrowhead in points, default is 10. |
| <span class="table-cell-nowrap">arrowSharp = *s*</span> | Specifies the continuously variable barb sharpness between -1.0 and 1. 0. |
|  |<table class="nested-table"><tbody><tr><td>*s*&nbsp;=1:</td><td>No barb; lines only.</td></tr><tr><td>*s*&nbsp;=0:</td><td>Blunt (default).</td></tr><tr><td>*s*&nbsp;=-1:</td><td>Diamond.</td></tr></tbody></table>
| <span class="table-cell-nowrap">arrowframe = *f*</span> | Specifies the stroke outline thickness of the arrow in Points. The default is f =0 for solid fill. |
| <span class="table-cell-nowrap">astyle = *s*</span> | Specifies which side of the line has barbs relative to a right-facing arrow. |
|  |<table class="nested-table"><tbody><tr><td>*s*&nbsp;=0:</td><td>None.</td></tr><tr><td>*s*&nbsp;=1:</td><td>Top.</td></tr><tr><td>*s*&nbsp;=2:</td><td>Bottom.</td></tr><tr><td>*s*&nbsp;=3:</td><td>Both (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">clipRect = (*left*, *top*, *right*, *bottom*)</span> |  |
|  | Clips drawing to the specifed rectangle. The clipRect keyword was added in Igor Pro 8.00. |
|  | *left*, *top*, *right*, and *bottom* are specified in the current coordinate system of the drawing environment. |
|  | If a save is in effect, you can use values of all 0 to cancel the clipping or, better, you can a use push, clipRect, save, drawing, pop sequence. When a save is in effect, the clipping is set once and remains unchanged for the remaining objects even if the coordinate system is changed. |
| <span class="table-cell-nowrap">dash = *dsh*</span> | *dsh* is a dash pattern number between 0 and 17 (see [SetDashPattern](/igorpro/commands/setdashpattern.md) for patterns). 0 (solid line) is the default. |
| <span class="table-cell-nowrap">fillbgc = (*r*,*g*,*b*[,*a*])</span> | Specifies fill background color. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is the window's background color. |
| <span class="table-cell-nowrap">fillfgc = (*r*,*g*,*b*[,*a*])</span> | Specifies fill foreground color. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque white. |
| <span class="table-cell-nowrap">fillpat = *fpatt*</span> | Specifies fill pattern density. |
|  |<table class="nested-table"><tbody><tr><td>*fpatt*&nbsp;=-1</td><td>Erase to background color.</td></tr><tr><td>*fpatt*&nbsp;=0:</td><td>No fill.</td></tr><tr><td>*fpatt*&nbsp;=1:</td><td>100% (solid pattern, the default).</td></tr><tr><td>*fpatt*&nbsp;=2:</td><td>75% gray.</td></tr><tr><td>*fpatt*&nbsp;=3:</td><td>50% gray.</td></tr><tr><td>*fpatt*&nbsp;=4:</td><td>25% gray.</td></tr></tbody></table>
| fillRule=*fr* |<table class="nested-table"><tbody><tr><td>*fr*&nbsp;=0:</td><td>Winding rule (default)</td></tr><tr><td>*fr*&nbsp;=1:</td><td>Even-odd rule</td></tr></tbody></table>
|  | The fillRule keyword applies only to polygons created with [DrawPoly](/igorpro/commands/drawpoly.md) and [DrawBezier](/igorpro/commands/drawbezier.md), not to those created manually. |
|  | See [Polygon and Bezier Curve Fill Rules](/igorpro/graphing/drawing.md#polygon-and-bezier-curve-fill-rules) for a discussion of the rules used for filling polygons and Bezier curves with intersecting edges. |
|  | The fillRule keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">fname = *"fontName"*</span> | Sets font name, default is the default font or the graph font. |
| <span class="table-cell-nowrap">fsize = *size*</span> | Sets text size, default is 12 points. |
| <span class="table-cell-nowrap">fstyle = *fs*</span> | *fs* is a bitwise parameter with each bit controlling one aspect of the font style as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">gedit = *flag*</span> | Supplies optional edit flag for a group of objects. Use with gstart. |
|  |<table class="nested-table"><tbody><tr><td>*flag*&nbsp;=0:</td><td>Select entire group, moveable (default).</td></tr><tr><td>*flag*&nbsp;=1:</td><td>Individual components editable as if not grouped. Allows objects to be grouped by name but still be editable</td></tr></tbody></table>
| <span class="table-cell-nowrap">gname = *name*</span> | Supplies optional *name* for an object group. Use with gstart. |
| gradient | See [Gradient Fills](/igorpro/graphing/making-figures/graphics.md#gradient-fills) for parameters and details. |
| gradientExtra | See [Gradient Fills](/igorpro/graphing/making-figures/graphics.md#gradient-fills) for parameters and details. |
| gstart | Marks the start of a group of objects. |
| gstop | Marks the end of a group of objects. |
| <span class="table-cell-nowrap">linebgc = (*r*,*g*,*b*[,*a*])</span> | Specifies line background color. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is the window's background color. |
| <span class="table-cell-nowrap">linecap = *cap*</span> | Sets the line end cap style: |
|  |<table class="nested-table"><tbody><tr><td>*cap*&nbsp;=0:</td><td>Flat caps (default)</td></tr><tr><td>*cap*&nbsp;=1:</td><td>Round caps</td></tr><tr><td>*cap*&nbsp;=2:</td><td>Square caps</td></tr></tbody></table>
|  | See [Line Join and End Cap Styles](/igorpro/graphing/making-figures/graphics.md#line-join-and-end-cap-styles) for further information. |
|  | linecap was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">linefgc = (*r*,*g*,*b*[,*a*])</span> | Specifies line foreground color. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
| <span class="table-cell-nowrap">linejoin = *j*</span> | Sets the line join style: |
|  |<table class="nested-table"><tbody><tr><td>*j*&nbsp;=0:</td><td>Miter joins</td></tr><tr><td>*j*&nbsp;=1:</td><td>Round joins</td></tr><tr><td>*j*&nbsp;=2:</td><td>Bevel joins (default)</td></tr></tbody></table>
|  | For a miter join, you can also set the miter limit using the *lineMiterLimit* keyword. |
|  | See [Line Join and End Cap Styles](/igorpro/graphing/making-figures/graphics.md#line-join-and-end-cap-styles) for further information. |
|  | linejoin was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">lineMiterLimit = *ml*</span> | Applies only to a miter line join style. See the *linejoin* keyword. |
|  |<table class="nested-table"><tbody><tr><td>*ml*&nbsp;&gt;=&nbsp;1:</td><td>Sets miter limit to *ml*</td></tr><tr><td>*ml*&nbsp;=&nbsp;INF:</td><td>Sets miter limit to unlimited</td></tr><tr><td>*ml*&nbsp;=&nbsp;0:</td><td>Leaves miter limit unchanged</td></tr><tr><td>*ml*&nbsp;=&nbsp;-1:</td><td>Sets miter limit to default (10)</td></tr></tbody></table>
|  | See [Line Join and End Cap Styles](/igorpro/graphing/making-figures/graphics.md#line-join-and-end-cap-styles) for further information. |
|  | lineMiterLimit was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">linethick = *thick*</span> | *thick* is a line thickness >= 0, default is 1 point. |
| <span class="table-cell-nowrap">origin = *x0*,*y0*</span> | Moves coordinate system origin to *x0*,*y0*. Unlike translate, rotate, and scale, this survives a change in coordinate system and is most useful that way. See ***Coordinate Transformation*** below. |
| pop | Pops a draw environment from the stack. Pops should always match pushes. |
| push | Pushes the current draw environment onto a stack (limited to 10). |
| <span class="table-cell-nowrap">rotate = *deg*</span> | Rotates coordinate system by *deg* degrees. Only makes sense if X and Y coordinate systems are the same. See ***Coordinate Transformation*** below. |
| <span class="table-cell-nowrap">rounding = *rnd*</span> | Radius for rounded rectangles in points, default is 10. |
| rsabout | Redefines coordinate system rotation or scaling to occur at the translation point instead of the current origin. To use, combine rotate or scale with translate and rsabout parameters. |
| save | Stores the current drawing environment as the default environment. |
| <span class="table-cell-nowrap">scale = *sx*,*sy*</span> | Scales coordinate system by *sx* and *sy*. Affects only coordinates -- not line thickness or arrow head sizes. See ***Coordinate Transformation*** below. |
| <span class="table-cell-nowrap">subpaths = *sp*</span> | Controls the way polygon and Bezier curve segments separated by NaN values are drawn. |
| <span class="table-cell-nowrap">*sp* = 0:</span> | Each segment is drawn as a separate polygon or Bezier curve, and any arrows are added to each segment as if they are separate polygons or Bezier curves. This is the default if you omit the subpaths keyword. |
| <span class="table-cell-nowrap">*sp* = 1:</span> | The segments are treated as subpaths within a single polygon or Bezier curve, making it possible to define a shape with holes. Any arrows are added only to the first or last points in the entire shape. |
|  | The subpaths keyword applies only to polygons and Bezier curves created with [DrawPoly](/igorpro/commands/drawpoly.md) and [DrawBezier](/igorpro/commands/drawbezier.md), not to those created manually. |
|  | Also see the fillRule keyword. |
|  | The subpaths keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">textrgb = (*r*,*g*,*b*[,*a*])</span> | Specifies text color. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
| <span class="table-cell-nowrap">textrot = *rot*</span> | Text rotation in degrees. |
|  | *rot* is a value from -360 to 360. |
|  | 0 is normal (default) horizontal left-to-right text, |
|  | 90 is vertical bottom-to-top text, etc. |
| <span class="table-cell-nowrap">textxjust = *xj*</span> | Sets horizontal text alignment. |
|  |<table class="nested-table"><tbody><tr><td>*xj*&nbsp;=0:</td><td>Left aligned text (default).</td></tr><tr><td>*xj*&nbsp;=1:</td><td>Center aligned text.</td></tr><tr><td>*xj*&nbsp;=2:</td><td>Right aligned text.</td></tr></tbody></table>
| <span class="table-cell-nowrap">textyjust = *yj*</span> | Sets vertical text alignment. |
|  |<table class="nested-table"><tbody><tr><td>*yj*&nbsp;=0:</td><td>Bottom aligned text (default).</td></tr><tr><td>*yj*&nbsp;=1:</td><td>Middle aligned text.</td></tr><tr><td>*yj*&nbsp;=2:</td><td>Top aligned text.</td></tr></tbody></table>
| <span class="table-cell-nowrap">translate = *dx*,*dy*</span> | Shifts coordinate system by *dx* and *dy*. Units are in the current coordinate system. See ***Coordinate Transformation*** below. |
| <span class="table-cell-nowrap">xcoord = abs</span> | X coordinates are absolute window coordinates. The unit of measurement is [control panel units](/igorpro/user-interface/controls.md#control-panel-units) if the window is a panel, otherwise they are points. xcoord=abs is the default for all windows except graphs where the default is xcoord=prel. The left edge of the window (or of the printable area in a layout) is where x=0. See [Drawing Coordinate Systems](/igorpro/graphing/drawing.md#drawing-coordinate-systems) for details. |
| <span class="table-cell-nowrap">xcoord = axrel</span> | X coordinates are relative axis rectangle coordinates (graphs only). The axrel coordinate system was added in Igor Pro 9.00. |
|  | The axis rectangle is the plot rectangle expanded to include any axis standoff. x=0 is at the left edge of the rectangle; x=1 is at the right edge of the rectangle. This coordinate system ideal for objects that should maintain their size and location relative to the axes when axis standoff is used. See [Axis Relative (Graphs Only)](/igorpro/graphing/drawing.md#axis-relative-graphs-only) for details. |
|  | You can retrieve the axis rectangle's coordinates using GetWindow axSize. |
| <span class="table-cell-nowrap">xcoord = rel</span> | X coordinates are relative window coordinates. x=0 is at the left edge of the window; x=1 is at the right edge. See [Drawing Coordinate Systems](/igorpro/graphing/drawing.md#drawing-coordinate-systems) for details. |
| <span class="table-cell-nowrap">xcoord = prel</span> | X coordinates are relative plot rectangle coordinates (graphs only). x=0 is at the left edge of the rectangle; x=1 is at the right edge of the rectangle. This coordinate system ideal for objects that should maintain their size and location relative to the axes, and is the default for graphs. See [Plot Relative (Graphs Only)](/igorpro/graphing/drawing.md#plot-relative-graphs-only) for details. |
|  | You can retrieve the plot rectangle's coordinates using GetWindow pSize. |
| <span class="table-cell-nowrap">xcoord = *axisName*</span> | X coordinates are in terms of the named axis (graphs only). |
| <span class="table-cell-nowrap">ycoord = abs</span> | Y coordinates are absolute window coordinates. The unit of measurement is [control panel units](/igorpro/user-interface/controls.md#control-panel-units) if the window is a panel, otherwise they are points. ycoord=abs is the default for all windows except graphs where the default is ycoord=prel. The top edge of the window (or the of the printable area in a layout) is where y=0. See [Drawing Coordinate Systems](/igorpro/graphing/drawing.md#drawing-coordinate-systems) for details. |
| <span class="table-cell-nowrap">ycoord = axrel</span> | Y coordinates are relative axis rectangle coordinates (graphs only).  The axrel coordinate system was added in Igor Pro 9.00. |
|  | The axis rectangle is the plot rectangle expanded to include any axis standoff. y=0 is at the top edge of the rectangle; y=1 is at the bottom edge of the rectangle. This coordinate system ideal for objects that should maintain their size and location relative to the axes when axis standoff is used. See [Axis Relative (Graphs Only)](/igorpro/graphing/drawing.md#axis-relative-graphs-only) for details. |
|  | You can retrieve the axis rectangle's coordinates using GetWindow axSize. |
| <span class="table-cell-nowrap">ycoord = rel</span> | Y coordinates are relative window coordinates. y=0 is at the top edge of the window; y=1 is at the bottom edge. See [Drawing Coordinate Systems](/igorpro/graphing/drawing.md#drawing-coordinate-systems) for details. |
| <span class="table-cell-nowrap">ycoord = prel</span> | Y coordinates are relative plot rectangle coordinates (graphs only). y=0 is at the top edge of the rectangle; y=1 is at the bottom edge of the rectangle. This coordinate system ideal for objects that should maintain their size and location relative to the axes, and is the default for graphs. See [Plot Relative (Graphs Only)](/igorpro/graphing/drawing.md#plot-relative-graphs-only) for details. |
|  | You can retrieve the plot rectangle's coordinates using GetWindow pSize. |
| <span class="table-cell-nowrap">ycoord = *axisName*</span> | Y coordinates are in terms of the named axis (graphs only). |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Specifies the named window or subwindow for drawing. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Coordinate Transformation* {#coordinate-transformation}
The execution order for the translate, rotate, scale, and origin parameters is important. Translation followed by rotation is different than rotation followed by translation. When using multiple keywords in one SetDrawEnv operation, the order in which they are applied is origin, translate, rotate followed by scale regardless of the command order (with the exception of the rsabout parameter). Before using origin with the save keyword, you should use push to save the current draw environment and then use pop after drawing objects using the new origin.

### *Examples* {#examples}
Following is a simple example of arrow markers:


```igor
NewPanel
SetDrawEnv arrow= 1,arrowlen= 30,save
SetDrawEnv arrowsharp= 0.3
DrawLine 61,67,177,31
SetDrawEnv arrowsharp= 1
DrawLine 65,95,181,59
SetDrawEnv astyle= 1
DrawLine 69,123,185,87
SetDrawEnv arrowframe= 1
DrawLine 73,151,189,115
```

You can position objects in one coordinate system and then draw them in another with the origin keyword. In the following coordinate transformation example, we position arrows in axis units but size them in absolute units.


```igor
Make/O jack=sin(x/8)
Display jack
SetDrawEnv xcoord=bottom,ycoord=left,save
SetDrawEnv push
SetDrawEnv origin=50,0
SetDrawEnv xcoord=abs,ycoord=abs,arrow=1,arrowlen=20,arrowsharp=0.2,save
DrawLine 0,0,50,0	// arrow 50 points long pointing to the right
DrawLine 0,0,0,50	// arrow 50 points long pointing down
// now let's move over, rotate a bit and draw the same arrows:
SetDrawEnv translate=100,0
SetDrawEnv rotate=30,save
DrawLine 0,0,50,0
DrawLine 0,0,0,50
SetDrawEnv pop
```

Now try zooming in on the graph. You will see that the first pair of arrows always starts at 50 on the bottom axis and 0 on the left axis whereas the second pair is 100 points to the right of the first.

### *See Also* {#see-also}
[Drawing](/igorpro/graphing/drawing.md), [DrawAction](/igorpro/commands/drawaction.md)