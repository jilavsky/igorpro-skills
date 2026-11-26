---
description: "The AppendBoxPlot operation appends a box plot trace to the target or named graph. A box plot is a way to display a summary of the distribution of data values."
slug: /commands/appendboxplot
---

<div className="command-signature">

## <strong>AppendBoxPlot</strong>  [<em>axis</em> <em>flags</em> ][/W=<em>winName</em> /TN=<em>traceName</em> /VERT[=<em>doVert</em>] /CATL[=<em>doCatLabels</em>]] <em>wave</em>[, <em>wave</em>, ...] [<em>vs</em> <em>xWave</em>] {#appendboxplot}

</div>

The AppendBoxPlot operation appends a box plot trace to the target or named graph. A box plot is a way to display a summary of the distribution of data values. Another way to display a summary of data distribution is via a violin plot.

AppendBoxPlot was added in Igor Pro 8.00.

A box plot trace is treated within Igor as a single graph trace, and many of the operations such as removing from a graph or reordering traces work the same with a box plot trace as with any other graph trace.

:::note
There is no DisplayBoxPlot operation. Use Display followed by AppendBoxPlot.
:::

The data for a single box in a box plot trace comes from either one entire 1D wave or from a single column of a multi-column wave. The number of box plots in the trace is determined by either the number of 1D waves in the list of waves, or by the number of columns in the single multi-column wave. It is not permitted to mix 1D and multi-column waves.

You can list up to 100 individual 1D waves. If you want more boxes than 100 in a box plot trace you must use a multi-column wave or add to the list using the [AddWavesToBoxPlot](/igorpro/commands/addwavestoboxplot.md) operation.

If you do not provide *xWave*, each box plot is positioned on a numeric axis at X=0, 1, etc. If the data is in a multi-column wave, positioning comes by default from the X scaling of the matrix wave. Providing a numeric *xWave* allows you to position each box plot at an arbitrary position on the X axis. A text *xWave* displays the box plots using a category axis. If you use the /CATL flag with a multi-column wave, the result is a category X axis using the dimension labels as the category labels. See [Category Plots](/igorpro/graphing/category-plots.md) and [Dimension Labels](/igorpro/igor-basics/multidimensional-waves.md#dimension-labels).

*xWave* must have at least as many points as you have 1D Y waves or columns in a multi-column wave. Because a list of waves may become too long for the command line, you can use an *xWave* that is longer than the list. Use [AddWavesToBoxPlot](/igorpro/commands/addwavestoboxplot.md) to complete the list.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/L/R/B/T</span> | These axis flags are the same as used by [AppendToGraph](/igorpro/commands/appendtograph.md). |
| <span class="table-cell-nowrap">/CATL[ = *doCatLabels*]</span> |  |
|  | Use the column dimension labels to produce box plots on a category axis using the column dimension labels as the category labels. *doCatLabels* is 0 or 1 and /CATL is equivalent to /CATL=1. |
| <span class="table-cell-nowrap">/TN = *traceName*</span> | Allows you to provide a custom name for a trace. This is useful when displaying waves with the same name but from different data folders. See [User-Defined Trace Names](/igorpro/programming/programming.md#user-defined-trace-names) for details, except that the /TN flag for AppendBoxPlot comes in the normal position in the command, after the command name. |
| <span class="table-cell-nowrap">/VERT[ = *doVert*]</span> | Arranges the individual box plots vertically along the Y axis. *doVert* is 0 or 1 and /VERT is equivalent to /VERT=1. |
|  | /VERT is similar to ModifyGraph SwapXY but on a trace-by-trace basis. To make a box plot with horizontal boxes, use either ModifyGraph SwapXY or AppendBoxPlot/VERT. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Appends to the named graph window or subwindow. When omitted, AppendBoxPlot is directed to the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
Some aspects of the overall appearance of a box plot trace can be set using [ModifyGraph](/igorpro/commands/modifygraph.md). By default, the line color is black and markers for non-outlier data points are hollow circles 0.7 times the size of the normal trace marker. Using the Modify Box Plot dialog or the ModifyBoxPlot operation, you can choose to use trace color, line size, line dash style, marker and marker size as set by ModifyGraph just as for a regular trace. Detailed control of these characteristics for various parts of a box plot trace is provided by [ModifyBoxPlot](/igorpro/commands/modifyboxplot.md). Markers to represent outliers, far outliers, and non-outliers override the marker set by ModifyGraph.

### *Examples* {#examples}

```igor
// Demo vertical box plot
Make/O/N=(25,3) multicol         // A three-column wave with 25 rows
SetRandomSeed(.4)
multicol = gnoise(1)             // Three normally-distributed datasets
multicol[20][1] = 5              // A "far" outlier
multicol[13][2] = -4             // An outlier
Make/O/N=3/T labels              // A text wave to make a category plot
labels = "Dataset #"+num2str(p)  // Labels for the X axis of a category plot
Display; AppendBoxPlot multicol vs labels
```

<img src="Images/AppendBoxPlot/AppendBoxPlot_1.png" width="100%"/>


```igor
// Demo horizontal box plot
Make/O/N=50 ds1, ds2, ds3, ds4
Make/O/N=4 dsX
ds1 = gnoise(1)
ds2 = gnoise(2)
ds3 = logNormalNoise(0, 1)
ds4 = enoise(2)
dsX = p^2
Display; AppendBoxPlot ds1,ds2,ds3,ds4 vs dsX
ModifyGraph swapXY=1       // Horizontal boxes
ModifyGraph margin(top)=20 // Top margin may be too small
```

<img src="Images/AppendBoxPlot/AppendBoxPlot_2.png" width="100%"/>

### *See Also* {#see-also}
[Display](/igorpro/commands/display.md), [AppendToGraph](/igorpro/commands/appendtograph.md), [ModifyGraph](/igorpro/commands/modifygraph.md), [ModifyBoxPlot](/igorpro/commands/modifyboxplot.md), [Box Plots](/igorpro/graphing/graphs.md#box-plots), [Violin Plots](/igorpro/graphing/graphs.md#violin-plots)