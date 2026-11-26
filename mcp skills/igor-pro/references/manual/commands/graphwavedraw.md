---
description: "The GraphWaveDraw operation initiates drawing a curve composed of yWave vs xWave in the target or named graph."
slug: /commands/graphwavedraw
---

<div className="command-signature">

## <strong>GraphWaveDraw</strong>  [/W=<em>winName</em> /B/F[=<em>f</em> ]/L/M/O/R/T] [<em>yWave</em>, <em>xWave</em>] {#graphwavedraw}

</div>

The GraphWaveDraw operation initiates drawing a curve composed of *yWave* vs *xWave* in the target or named graph. The user draws the curve using the mouse, and the values are stored in a pair of waves as XY data.

The user can manually initiate drawing by selecting ShowTools from the Graph menu and clicking in the appropriate tool rather.

### *Parameters* {#parameters}
*yWave* and *xWave* can be simple names of waves in the current data folder or partial or full data folder paths to waves. If the waves already exist, GraphWaveDraw overwrites them. *yWave* and *xWave* can also be wave references pointing to existing waves in which case GraphWaveDraw overwrites them. Prior to Igor Pro 9.00, only simple names were accepted.

If *yWave* and *xWave* already exist, an error is generated unless you include the /O flag.

If you omit *yWave* and *xWave* then waves named W_YPoly*n* and W_XPoly*n* are created in the current data folder. *n* is an integer used to make the output wave names unique in their data folder, so Igor might create waves named W_XPoly0 and W_YPoly0, for example.

If there is no *yWave* vs *xWave* trace in the graph, GraphWaveDraw appends it.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/F[ = *f* ]</span> | Initiates freehand drawing. In normal drawing, you click where you want a data point. In freehand drawing, you click once and then draw with the mouse button held down. If present, *f* specifies the smoothing factor. Max value is 8 (which is really slow), min value is 0. The default is 0. The drawing tools use a value of 3 which is the recommended value. |
| <span class="table-cell-nowrap">/L/R/B/T</span> | Specifies which axes to use (Left, Right, Bottom, Top). Bottom and Left axes are used by default. Can specify free axes using /L=*axis name* type notation. See [AppendToGraph](/igorpro/commands/appendtograph.md) for details. If necessary, the specified axes will be created. If an axis is created its range is set to -1 to 1. |
| <span class="table-cell-nowrap">/M</span> | Specifies that the curve being edited must be monotonic in the X dimension. The user is not allowed drag points so that they cross horizontally. |
| <span class="table-cell-nowrap">/O</span> | Overwrites *yWave* and *xWave* if they already exist. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Draws in the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
Once drawing starts no other user actions are allowed.

In normal mode, drawing stops when you double-click or when you click on the first point (in which case the last point is set equal to the first point). When drawing finishes then the edit mode is entered.

In freehand mode, drawing stops when the mouse is released or when 10000 points have been drawn.

If you include /O and the waves are already on the graph then the first trace instance on the graph displaying them is used even if the trace uses a different pair of axes than specified by /L, /R, /B, and /T.

### *Output Variables* {#output-variables}

|  |  |
| --- | --- |
| S_xWave | Path to the X wave relative to the current data folder. S_xWave is create in Igor Pro 9.00 and later. |
| S_yWave | Path to the Y wave relative to the current data folder. S_yWave is create in Igor Pro 9.00 and later. |

### *See Also* {#see-also}
[GraphNormal](/igorpro/commands/graphnormal.md), [GraphWaveEdit](/igorpro/commands/graphwaveedit.md), [DrawAction](/igorpro/commands/drawaction.md)