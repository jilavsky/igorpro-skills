---
description: "The RemoveContour operation removes the traces, and releases memory associated with the contour of contourInstanceName in the target or named graph."
slug: /commands/removecontour
---

<div className="command-signature">

## <strong>RemoveContour</strong>  [/ALL /W=<em>winName</em> /Z] <em>contourInstanceName</em> [, <em>contourInstanceName</em> ]... {#removecontour}

</div>

The RemoveContour operation removes the traces, and releases memory associated with the contour of *contourInstanceName*  in the target or named graph.

### *Parameters* {#parameters}
*contourInstanceName* is usually simply the name of a wave. More precisely, *contourInstanceName* is a wave name, optionally followed by the # character and an instance number to identify which contour plot of a given wave is to be removed.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALL</span> | Removes all contour plots from the graph. Any contour name parameters listed are ignored. /ALL was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Removes contours from the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/Z</span> | Suppresses error if specified contour is not on the graph. /Z was added in Igor 10. |

### *Details* {#details}
If the axes used by the given contour plot are not in use after removing it, they will also be removed.

A contour instance name in a string can be used with the $ operator for *contourInstance*.

### *Examples* {#examples}

```igor
Display;AppendMatrixContour zw  // new graph, contour of zw matrix
AppendMatrixContour zw          // two contours of zw
RemoveContour zw#1              // remove the second contour
```