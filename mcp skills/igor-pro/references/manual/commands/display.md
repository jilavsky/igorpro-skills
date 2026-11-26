---
description: "The Display operation creates a new graph window or subwindow, and appends the named waves, if any. Waves are displayed as 1D traces."
slug: /commands/display
---

<div className="command-signature">

## <strong>Display</strong>  [/B[=<em>axisName</em> /HIDE=<em>h</em> /FG=(<em>gLeft</em>, <em>gTop</em>, <em>gRight</em>, <em>gBottom</em> ) /HOST=<em>hcSpec</em> /I /K=<em>k</em> /L[=<em>axisName</em>]/M /N=<em>name</em> /PG=(<em>gLeft</em>, <em>gTop</em>, <em>gRight</em>, <em>gBottom</em> )/R[=<em>axisName</em> ] /T[=<em>axisName</em> ] /VERT/W=(<em>left</em>, <em>top</em>, <em>right</em>, <em>bottom</em> )] [<em>waveName</em> [,<em>waveName</em> ] ... [<em>vs</em> <em>xwaveName</em> ]] [<em>as</em> <em>titleStr</em> ] {#display}

</div>

The Display operation creates a new graph window or subwindow, and appends the named waves, if any. Waves are displayed as 1D traces.

By default, waves are plotted versus the left and bottom axes. Use the /L, /B, /R, and /T flags to plot the waves against other axes.

### *Parameters* {#parameters}
Up to 100 *waveNames*  may be specified, subject to the 2500 byte command line length limit. If no wave names are specified, a blank graph is created and the axis flags are ignored.

If you specify "vs *xwaveName* ", the Y values of the named waves are plotted versus the Y values of *xwaveName*. If you don't specify "vs *xwaveName* ", the Y values of each *waveName*  are plotted versus its own X values.

If *xwaveName* is a text wave or the special keyword '\_labels\_', the resulting plot is a category plot (see [Category Plots](/igorpro/graphing/category-plots.md)). Each element of *waveName* is plotted by default in bars mode ([ModifyGraph](/igorpro/commands/modifygraph.md) mode=5) against a category labeled with the text of the corresponding element of *xwaveName* or the text of the dimension labels of the first Y wave.

The Y waves for a category plot should have point scaling (see [The Waveform Model of Data](/igorpro/igor-basics/waves.md#the-waveform-model-of-data) for information on wave scaling);  since this is what was intended, things work better that way. However, if all the Y waves have the same scaling, it will work correctly.

*titleStr* is a string expression containing the graph's title. If not specified, Igor will provide one which identifies the waves displayed in the graph.

Subsets of data, including individual rows or columns from a matrix, may be specified using [Subrange Display Syntax](/igorpro/graphing/graphs.md#subrange-display-syntax).

You can provide a custom name for a trace by appending /TN=traceName to the waveName specification. This is useful when displaying waves with the same name but from different data folders. See [Trace Name Parameters](/igorpro/programming/programming.md#trace-name-parameters) for more information.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B[ = *axisName* ]</span> | Plots X coordinates versus the standard or named bottom axis. |
| <span class="table-cell-nowrap">/FG = (*gLeft*, *gTop*, *gRight*, *gBottom* )</span> |  |
|  | Specifies the frame guide to which the outer frame of the subwindow is attached inside the host window. |
|  | The standard frame guide names are FL, FR, FT, and FB for the left, right, top, and bottom frame guides, respectively, or user-defined guide names as defined by the host. Use * to specify a default guide name. |
|  | Guides may override the numeric positioning set by /W. |
| <span class="table-cell-nowrap">/HIDE = *h*</span> | Hides (*h* = 1) or shows (*h* = 0, default) the window. |
| <span class="table-cell-nowrap">/HOST = *hcSpec*</span> | Embeds the new graph in the host window or subwindow specified by *hcSpec*. |
|  | When identifying a subwindow with *hcSpec*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/I</span> | specifies that /W coordinates are in inches. |
| <span class="table-cell-nowrap">/K = *k*</span> | Specifies window behavior when the user attempts to close it. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr><tr><td>*k*&nbsp;=3:</td><td>Hides the window.</td></tr><tr><td>*k*&nbsp;=4:</td><td>Kills with no dialog and is not saved with the experiment.</td></tr></tbody></table>
|  | If you use /K=2 or /K=3, you can still kill the window using the [KillWindow](/igorpro/commands/killwindow.md) operation. |
| <span class="table-cell-nowrap">/L[ = *axisName* ]</span> | Plots y coordinates versus the standard or named left axis. |
| <span class="table-cell-nowrap">/M</span> | Specifies that /W coordinates are in centimeters. |
| <span class="table-cell-nowrap">/N = *name*</span> | Requests that the created graph have this name, if it is not in use. If it is in use, then *name*0, *name*1, etc. are tried until an unused window name is found. In a function or macro, S_name is set to the chosen graph name. |
| <span class="table-cell-nowrap">/NCAT</span> | In Igor Pro 6.37 or later, allows later appending of a category trace to a numeric plot. See [Combining Numeric and Category Traces](/igorpro/graphing/category-plots.md#combining-numeric-and-category-traces) for details. |
| <span class="table-cell-nowrap">/PG = (*gLeft*, *gTop*, *gRight*, *gBottom* )</span> |  |
|  | Specifies the inner plot rectangle of the graph subwindow inside its host window. |
|  | The standard plot rectangle guide names are PL, PR, PT, and PB, for the left, right, top and bottom plot rectangle guides, respectively, or user-defined guide names as defined by the host. Use * to specify a default guide name. |
|  | Guides may override the numeric positioning set by /W. |
| <span class="table-cell-nowrap">/R = [*axisName* ]</span> | Plots Y coordinates versus the standard or named right axis. |
| <span class="table-cell-nowrap">/T = [*axisName* ]</span> | Plots Y coordinates versus the standard or named top axis. |
| <span class="table-cell-nowrap">/TN = *traceName*</span> | Allows you to provide a custom name for a trace. This is useful when displaying waves with the same name but from different data folders. See [User-Defined Trace Names](/igorpro/programming/programming.md#user-defined-trace-names) for details. |
| <span class="table-cell-nowrap">/VERT</span> | Plots data vertically. Similar to SwapXY ([ModifyGraph](/igorpro/commands/modifygraph.md)) but on a trace-by-trace basis. |
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom* )</span> |  |
|  | Gives the graph a specific location and size on the screen. Coordinates for /W are in points unless /I or /M are specified before /W. |
|  | When used with the /HOST flag, the specified location coordinates can have one of two possible meanings: |
|  |<table class="nested-table"><tbody><tr><td>1.</td><td>When all values are less than 1, coordinates are assumed to be fractional relative to the host frame size.</td></tr><tr><td>2.</td><td>When any value is greater than 1, coordinates are taken to be fixed locations measured in points, or [control panel units](/igorpro/user-interface/controls.md#control-panel-units) for control panel hosts, relative to the top left corner of the host frame.</td></tr></tbody></table>
|  | When the subwindow position is fully specified using guides (using the /HOST, /FG, or /PG flags), the /W flag may still be used although it is not needed. |

### *Details* {#details}
If /N is not used, Display automatically assigns to the graph a name of the form "Graph*n* ", where *n*  is some integer. In a function or macro, the assigned name is stored in the S_name string. This is the name you can use to refer to the graph from a procedure. Use the [RenameWindow](/igorpro/commands/renamewindow.md) operation to rename the graph.

### *Examples* {#examples}
To make a contour plot, use:


```igor
Display; AppendMatrixContour waveName
```

or


```igor
Display; AppendXYZContour waveName
```

To display an image, use:


```igor
Display; AppendImage waveName
```

or


```igor
NewImage waveName
```

### *See Also* {#see-also}
[AppendToGraph](/igorpro/commands/appendtograph.md)

To make a contour plot, use Display; [AppendMatrixContour](/igorpro/commands/appendmatrixcontour.md) or Display; [AppendXYZContour](/igorpro/commands/appendxyzcontour.md).

To display an image, use [NewImage](/igorpro/commands/newimage.md). or Display;[AppendImage](/igorpro/commands/appendimage.md).

Use [ModifyGraph](/igorpro/commands/modifygraph.md) to alter the appearance of traces, axes, etc.