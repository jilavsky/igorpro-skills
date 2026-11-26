---
description: "Adds additional 1D waves to a pre-existing box plot trace created by AppendBoxPlot."
slug: /commands/addwavestoboxplot
---

<div className="command-signature">

## <strong>AddWavesToBoxPlot</strong>  [/W=<em>winName</em> /T=<em>traceName</em> /INST=<em>traceInstance</em>] <em>wave</em> [, <em>wave</em> ] ... {#addwavestoboxplot}

</div>

Adds additional 1D waves to a pre-existing box plot trace created by [AppendBoxPlot](/igorpro/commands/appendboxplot.md).

AddWavesToBoxPlot was added in Igor Pro 8.00.

Because a box plot trace may require a number of waves to define each dataset in the trace, and because wave names may be quite long, the AddWavesToBoxPlot operation is provided to add waves to a list begun by AppendBoxPlot.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/T = *traceName*</span> |  |
| <span class="table-cell-nowrap">/INST = *traceInstance*</span> |  |
|  | These flags specify the name and instance number of an existing box plot trace to which waves will be added. You can use /T without /INST, in which case a trace with instance number zero will be used. Do not use /INST without /T. |
|  | See [Creating Graphs](/igorpro/graphing/graphs.md#creating-graphs) for information about trace names and trace instance numbers. |
|  | In the absence of both /T and /INST, the default is to use the top box plot trace found on the graph. That would be the most recently added box plot trace. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Appends to the named graph window or subwindow. When omitted, AddWavesToBoxPlot operates on the active window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
If your original AppendBoxPlot command included an X wave, the total number of waves in the list of box plot dataset waves cannot be greater than the number of points in your X wave.

If the box plot trace is defined by a multicolumn wave, you cannot add additional waves using this operation.

### *See Also* {#see-also}
[Box Plots](/igorpro/graphing/graphs.md#box-plots), [AppendBoxPlot](/igorpro/commands/appendboxplot.md), [ModifyBoxPlot](/igorpro/commands/modifyboxplot.md)