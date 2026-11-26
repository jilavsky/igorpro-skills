---
description: "The AppendViolinPlot operation appends a violin plot trace to the target or named graph."
slug: /commands/appendviolinplot
---

<div className="command-signature">

## <strong>AppendViolinPlot</strong>  [<em>axis</em> <em>flags</em> ][/W=<em>winName</em> /TN=<em>traceName</em> /VERT[=<em>doVert</em>] /CATL[=<em>doCatLabels</em>]] <em>wave</em>[, <em>wave</em>, ...] [<em>vs</em> <em>xWave</em>] {#appendviolinplot}

</div>

The AppendViolinPlot operation appends a violin plot trace to the target or named graph. A violin plot (also called a "bean plot") is a way to display a summary of the distribution of data values using a kernel density estimator curve (see [StatsKDE](/igorpro/commands/statskde.md)). Another way to display a summary of data distribution is via a box plot.

AppendViolinPlot was added in Igor Pro 8.00.

A violin plot trace is treated within Igor as a single graph trace, and many of the operations such as removing from a graph or reordering traces work the same with a violin plot trace as with any other graph trace.

:::note
There is no DisplayViolinPlot operation. Use Display followed by AppendViolinPlot.
:::

### *Parameters* {#parameters}

The data for a single violin plot in a violin plot trace comes from either one entire 1D wave or from a single column of a multi-column wave. The number of violin plots in the trace is determined by either the number of 1D waves in the list of waves, or by the number of columns in the single multi-column wave. It is not permitted to mix 1D and multi-column waves.

You can list up to 100 individual 1D waves. If you want more violin plots than 100 in a violin plot trace you must use a multi-column wave or add to the list using the [AddWavesToViolinPlot](/igorpro/commands/addwavestoviolinplot.md) operation.

If you do not provide *xWave*, each violin plot is positioned on a numeric axis at X=0, 1, etc. If the data is in a multi-column wave, positioning comes by default from the X scaling of the matrix wave. Providing a numeric *xWave* allows you to position each violin plot at an arbitrary position on the X axis. A text *xWave* displays the violin plots using a category axis. If you use the /CATL flag with a multi-column wave, the result is a category X axis using the dimension labels as the category labels. See [Category Plots](/igorpro/graphing/category-plots.md) and [Dimension Labels](/igorpro/igor-basics/multidimensional-waves.md#dimension-labels).

*xWave* must have at least as many points as you have 1D Y waves or columns in a multi-column wave. Because a list of waves may become too long for the command line, you can use an *xWave* that is longer than the list. Use [AddWavesToViolinPlot](/igorpro/commands/addwavestoviolinplot.md) to complete the list.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/L/R/B/T</span> | These axis flags are the same as used by [AppendToGraph](/igorpro/commands/appendtograph.md). |
| <span class="table-cell-nowrap">/CATL[ = *doCatLabels*]</span> |  |
|  | Use the column dimension labels to produce violin plots on a category axis using the column dimension labels as the category labels. *doCatLabels* is 0 or 1 and /CATL is equivalent to /CATL=1. |
| <span class="table-cell-nowrap">/TN = *traceName*</span> | Allows you to provide a custom name for a trace. This is useful when displaying waves with the same name but from different data folders. See [User-Defined Trace Names](/igorpro/programming/programming.md#user-defined-trace-names) for details, except that the /TN flag for AppendViolinPlot comes in the normal position in the command, after the command name. |
| <span class="table-cell-nowrap">/VERT[ = *doVert*]</span> | Arranges the individual violin plots vertically along the Y axis. *doVert* is 0 or 1 and /VERT is equivalent to /VERT=1. |
|  | /VERT is similar to ModifyGraph SwapXY but on a trace-by-trace basis. To make a violin plot oriented horizontally, use either ModifyGraph SwapXY or AppendViolinPlot/VERT. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Appends to the named graph window or subwindow. When omitted, AppendViolinPlot is directed to the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
Some aspects of the overall appearance of a violin plot trace can be set using [ModifyGraph](/igorpro/commands/modifygraph.md). By default, the line color is black and markers for non-outlier data points are hollow circles half the size of the normal trace marker. Using the Modify Violin Plot dialog or the ModifyViolinPlot operation, you can choose to use trace color, line size, line dash style, marker and marker size as set by ModifyGraph just as for a regular trace. Detailed control of these characteristics for various parts of a violin plot trace is provided by [ModifyViolinPlot](/igorpro/commands/modifyviolinplot.md).

### *Examples* {#examples}

```igor
Make/O/N=(25,3) multicol        // A three-column wave with 25 rows
SetRandomSeed(.5)
multicol = gnoise(1)            // Three normally-distributed datasets
Make/O/N=3/T labels             // A text wave to make a category plot
labels = "Dataset #"+num2str(p) // Labels for the X axis of a category plot
Display;AppendViolinPlot multicol vs labels
```

<img src="Images/AppendViolinPlot/AppendViolinPlot_0.png" width="100%"/>


```igor
Make/O/N=50 ds1, ds2, ds3, ds4
Make/O/N=4 dsX
ds1 = gnoise(1)
ds2 = gnoise(2)
ds3 = logNormalNoise(0, 1)
ds4 = enoise(2)
dsX = p^2
Display;AppendViolinPlot ds1,ds2,ds3,ds4 vs dsX
ModifyGraph swapXY=1        // Horizontal boxes
ModifyGraph margin(top)=20  // Top margin may be too small
```

<img src="Images/AppendViolinPlot/AppendViolinPlot_1.png" width="100%"/>



### *See Also* {#see-also}
[Display](/igorpro/commands/display.md), [AppendToGraph](/igorpro/commands/appendtograph.md), [ModifyGraph](/igorpro/commands/modifygraph.md), [ModifyViolinPlot](/igorpro/commands/modifyviolinplot.md), [Box Plots](/igorpro/graphing/graphs.md#box-plots), [Violin Plots](/igorpro/graphing/graphs.md#violin-plots)