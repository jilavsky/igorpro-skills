---
description: "The ToolsGrid operation controls the grid you can use for laying out draw or control objects."
slug: /commands/toolsgrid
---

<div className="command-signature">

## <strong>ToolsGrid</strong>  [/W=<em>winName</em> ] <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] {#toolsgrid}

</div>

The ToolsGrid operation controls the grid you can use for laying out draw or control objects.

### *Parameters* {#parameters}
ToolsGrid can accept multiple *keyword* = *value* parameters on one line.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">snap = *n*</span> | Turns snap to grid on (*n* =1) or off (*n* =0). |
| <span class="table-cell-nowrap">visible = *n*</span> | Turns on grid visibility (*n* =1) or hides it (*n* =0). |
| <span class="table-cell-nowrap">grid = (*xy0*,*dxy*,*ndiv*)</span> | Defines both X and Y grids where *ndiv* is the number of subdivisions between major grid lines and *xy0* and *dxy* define the origin and spacing. Units are in points. |
| <span class="table-cell-nowrap">gridx = (*x0*,*dx*,ndiv )</span> | Defines the X grid where *ndiv* is the number of subdivisions between major grid lines and *x0* and *dx* define the origin and spacing. Units are in points. |
| <span class="table-cell-nowrap">gridy = (*y0*,*dy*,*ndiv*)</span> | Defines the Y grid where *ndiv* is the number of subdivisions between major grid lines and *y0* and *dy* define the origin and spacing. Units are in points. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Sets the named window or subwindow for drawing. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with winName, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
The default grid is 1 inch with 8 subdivisions. The grid is visible only in draw or selector mode and appears in front of the currently active draw layer.