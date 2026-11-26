---
description: "The AppendToGraph operation appends the named waves as traces in the target or named graph. By default the traces are plotted versus the left and bottom axes."
slug: /commands/appendtograph
---

<div className="command-signature">

## <strong>AppendToGraph</strong>  [/W=<em>winName</em> /B[=<em>axisName</em> ] /C=(<em>r</em>,<em>g</em>,<em>b</em>[,<em>a</em>]) /L[=<em>axisName</em> ] /NCAT/Q/R [=<em>axisName</em> ] /T[=<em>axisName</em> ]/VERT] <em>waveName</em>  [, <em>waveName</em> ] ... [<em>vs</em> <em>xwaveName</em> ] {#appendtograph}

</div>

The AppendToGraph operation appends the named waves as traces in the target or named graph. By default the traces are plotted versus the left and bottom axes.

### *Parameters* {#parameters}
*waveNames*  are the names of existing waves.

vs *xwaveName*  tells Igor to plot the data values of *waveNames*  against the data values of *xwaveName*. Otherwise, the data values of *waveName* are plotted versus calculated X values derived from the X scaling of *waveName*.

If you are appending a new trace to an existing category plot, *xwaveName* must be the same as the one already controlling the plot's X axis. If the existing X axis uses dimension labels from a Y wave, using the '\_labels\_' keyword, then *xwaveName* must be set to '\_labels\_'.

If you are appending a new category plot using a different X axis, *xwaveName* can refer any suitable text wave, or it may be '\_labels\_' to use dimension labels from the Y wave.

Subsets of data, including individual rows or columns from a matrix, may be specified using [Subrange Display Syntax](/igorpro/graphing/graphs.md#subrange-display-syntax).

You can provide a custom name for a trace by appending /TN=traceName to the waveName specification. This is useful when displaying waves with the same name but from different data folders. See [Trace Name Parameters](/igorpro/programming/programming.md#trace-name-parameters) for more information.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B[ = *axisName* ]</span> | Plots X coordinates versus the standard or named bottom axis. |
| <span class="table-cell-nowrap">/C = (*r*,*g*,*b*[,*a*])</span> | Sets the color of appended traces. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">/L[ = *axisName* ]</span> | Plots Y coordinates versus the standard or named left axis. |
| <span class="table-cell-nowrap">/NCAT</span> | Causes trace to be plotted normally on what otherwise is a category plot. X values are just category numbers but can be fractional. Category numbers start from zero. This can be used to overlay the original data points for a box plot. |
|  | See [Combining Numeric and Category Traces](/igorpro/graphing/category-plots.md#combining-numeric-and-category-traces) for details. |
| <span class="table-cell-nowrap">/Q</span> | If appending to a pair of existing axes then a special, quick update mode is used. A side effect of this mode is that waves that are appended are marked as not modified. This will prevent other graphs containing these waves, if any, from being updated properly. |
| <span class="table-cell-nowrap">/R[ = *axisName* ]</span> | Plots Y coordinates versus the standard or named right axis. |
| <span class="table-cell-nowrap">/T[ = *axisName* ]</span> | Plots X coordinates versus the standard or named top axis. |
| <span class="table-cell-nowrap">/TN = *traceName*</span> |  |
|  | Allows you to provide a custom name for a trace. This is useful when displaying waves with the same name but from different data folders. See [User-Defined Trace Names](/igorpro/programming/programming.md#user-defined-trace-names) for details. |
| <span class="table-cell-nowrap">/VERT</span> | Plots data vertically. Similar to SwapXY ([ModifyGraph](/igorpro/commands/modifygraph.md)) but on a trace-by-trace basis. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Appends to the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *See Also* {#see-also}
[Display](/igorpro/commands/display.md), [ModifyGraph](/igorpro/commands/modifygraph.md)