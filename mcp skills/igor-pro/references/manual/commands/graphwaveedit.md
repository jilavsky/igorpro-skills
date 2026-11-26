---
description: "The GraphWaveEdit operation initiates editing a wave trace in a graph. The wave trace must already be in the graph."
slug: /commands/graphwaveedit
---

<div className="command-signature">

## <strong>GraphWaveEdit</strong>  [/M /NI /ND /T=<em>t</em>  /W=<em>winName</em> ] <em>traceName</em> {#graphwaveedit}

</div>

The GraphWaveEdit operation initiates editing a wave trace in a graph. The wave trace must already be in the graph.

Normally, you would initiate editing by selecting ShowTools from the Graph menu and clicking in the appropriate tool rather than using GraphWaveEdit.

### *Parameters* {#parameters}
*traceName*  is a wave name, optionally followed by the # character and an instance number: "myWave#1" is the second instance of myWave appended to the graph ("myWave" is the first).

A string containing *traceName* can be used with the $ operator to specify *traceName*.

If *traceName*  is omitted then you get to pick the wave trace to edit by clicking on it.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/M</span> | Specifies that the edited trace must be monotonic in the X dimension. You cannot drag points so that they cross horizontally. |
| <span class="table-cell-nowrap">/ND</span> | Suppresses deletion of a data point when the user presses Alt and clicks on the point. |
| <span class="table-cell-nowrap">/NI</span> | Suppresses insertion of a new data point when the user clicks between points. |
| <span class="table-cell-nowrap">/T = *t*</span> | Sets the trace mode. |
|  |<table class="nested-table"><tbody><tr><td>*t*&nbsp;=0:</td><td>Lines and small square markers (default).</td></tr><tr><td>*t*&nbsp;=1:</td><td>User settings unchanged.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/W = *winName*</span> | Edits traces in the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
The GraphWaveEdit operation is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

### *See Also* {#see-also}
[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)

[GraphNormal](/igorpro/commands/graphnormal.md), [GraphWaveDraw](/igorpro/commands/graphwavedraw.md), [DrawAction](/igorpro/commands/drawaction.md)