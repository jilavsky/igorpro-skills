---
description: "The NewWaterfall operation creates a new waterfall plot window or subwindow using each column in the 2D matrix wave as a waterfall trace."
slug: /commands/newwaterfall
---

<div className="command-signature">

## <strong>NewWaterfall</strong>  [/FG=(<em>gLeft</em>, <em>gTop</em>, <em>gRight</em>, <em>gBottom</em> )/HIDE=<em>h</em> /HOST=<em>hcSpec</em> /I /K=<em>k</em> /M /N=<em>name</em> /PG=(<em>gLeft</em>, <em>gTop</em>, <em>gRight</em>, <em>gBottom</em> )/W=(<em>left</em>,<em>top</em>,<em>right</em>,<em>bottom</em> )] <em>matrixWave</em>  [<em>vs</em> {<em>xWave</em>,<em>yWave</em> }] {#newwaterfall}

</div>

The NewWaterfall operation creates a new waterfall plot window or subwindow using each column in the 2D matrix wave as a waterfall trace.

You can manually set X and Y scaling by specifying *xWave* and *yWave* to override the default scalings. Either *xWave* or *yWave* may be omitted by using a \*.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/FG = (*gLeft*, *gTop*, *gRight*, *gBottom* )</span> |  |
|  | Specifies the frame guide to which the outer frame of the subwindow is attached inside the host window. |
|  | The standard frame guide names are FL, FR, FT, and FB for the left, right, top, and bottom frame guides, respectively, or user-defined guide names as defined by the host. Use \* to specify a default guide name. |
|  | Guides may override the numeric positioning set by /W. |
| <span class="table-cell-nowrap">/HIDE = *h*</span> | Hides (*h* = 1) or shows (*h* = 0, default) the window. |
| <span class="table-cell-nowrap">/HOST = *hcSpec*</span> | Embeds the new waterfall plot in the host window or subwindow specified by *hcSpec*. |
|  | When identifying a subwindow with *hcSpec*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/I</span> | Sets window coordinates to inches. |
| <span class="table-cell-nowrap">/K = *k*</span> | Specifies window behavior when the user attempts to close it. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr><tr><td>*k*&nbsp;=3:</td><td>Hides the window.</td></tr><tr><td>*k*&nbsp;=4:</td><td>Kills with no dialog and is not saved with the experiment.</td></tr></tbody></table>
|  | If you use /K=2 or /K=3, you can still kill the window using the [KillWindow](/igorpro/commands/killwindow.md) operation. |
| <span class="table-cell-nowrap">/M</span> | Sets window coordinates to centimeters. |
| <span class="table-cell-nowrap">/N = *name*</span> | Requests that the created waterfall plot window have this name, if it is not in use. If it is in use, then *name*0, *name*1, etc are tried until an unused window name is found. In a function or macro, S_name is set to the chosen name. |
| <span class="table-cell-nowrap">/PG = (*gLeft*, *gTop*, *gRight*, *gBottom* )</span> |  |
|  | Specifies the inner plot rectangle of the waterfall plot subwindow inside its host window. |
|  | The standard plot rectangle guide names are PL, PR, PT, and PB, for the left, right, top and bottom plot rectangle guides, respectively, or user-defined guide names as defined by the host. Use * to specify a default guide name. |
|  | Guides may override the numeric positioning set by /W. |
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom*)</span> |  |
|  | Specifies window size. Coordinates are in points unless /I or /M is specified before /W. |
|  | When used with the /HOST flag, the specified location coordinates can have one of two possible meanings: |
|  |<table class="nested-table"><tbody><tr><td>1.</td><td>When all values are less than 1, coordinates are assumed to be fractional relative to the host frame size.</td></tr><tr><td>2.</td><td>When any value is greater than 1, coordinates are taken to be fixed locations measured in points, or [control panel units](/igorpro/user-interface/controls.md#control-panel-units) for control panel hosts, relative to the top left corner of the host frame.</td></tr></tbody></table>
| When the subwindow position is fully specified using guides (using the <span class="table-cell-nowrap">/HOST,</span> <span class="table-cell-nowrap">/FG,</span> or <span class="table-cell-nowrap">/PG</span> flags), the <span class="table-cell-nowrap">/W</span> flag may still be used although it is not needed. |  |

### *Details* {#details}
The X and Z axes are always at the bottom and left, whereas the Y axis runs at a default 45 degrees along the right-hand side. The angle and length of the Y axis can be changed using the ModifyWaterfall operation. Other features of the graph can be changed using normal graph operations.

Each column from *matrixWave* is plotted in, and clipped by, a rectangle defined by the X and Z axes with the rectangle displaced along the angled Y axis as a function of the Y value.

Except when hidden lines are active, the traces are drawn from back to front.

To modify certain properties of a waterfall plot, you need to use the ModifyWaterfall operation. For other properties, use the usual axis and trace dialogs.

### *See Also* {#see-also}
[Waterfall Plots](/igorpro/graphing/graphs.md#waterfall-plots), [ModifyWaterfall](/igorpro/commands/modifywaterfall.md), [ModifyGraph](/igorpro/commands/modifygraph.md)