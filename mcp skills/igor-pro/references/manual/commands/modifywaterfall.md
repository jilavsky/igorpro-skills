---
description: "The ModifyWaterfall operation modifies the properties of the waterfall plot in the top or named graph."
slug: /commands/modifywaterfall
---

<div className="command-signature">

## <strong>ModifyWaterfall</strong>  [/W=<em>winName</em> ] <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em>  ...] {#modifywaterfall}

</div>

The ModifyWaterfall operation modifies the properties of the waterfall plot in the top or named graph.

### *Parameters* {#parameters}
*keyword* is one of the following:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">angle = *a*</span> | Angle in degrees from horizontal of the angled y axis (*a*=10 to 90). |
| <span class="table-cell-nowrap">axlen = *len*</span> | Relative length of angled y axis. *len* is a fraction between 0.1 and 0.9. |
| hidden= *h* |<table class="nested-table"><tbody><tr><td>*h*&nbsp;=0:</td><td>Turns hidden line off.</td></tr><tr><td>*h*&nbsp;=1:</td><td>Uses painter&#39;s algorithm.</td></tr><tr><td>*h*&nbsp;=2:</td><td>True hidden.</td></tr><tr><td>*h*&nbsp;=3:</td><td>Hides lines with bottom removed.</td></tr><tr><td>*h*&nbsp;=4:</td><td>Hides lines using a different color for the bottom. When specified, the top color is the normal color for lines and the bottom color is set using ModifyGraph negRGB=(r,g,b[,*a*]).</td></tr></tbody></table>
|  | <div><Admonition type="note"><p>Hidden lines are active only when the mode is lines between points.</p></Admonition></div> |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Modifies waterfall plot in the named graph window or subwindow. When omitted, action will affect the active window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
Painter's algorithm draws the traces from back to front and erases hidden lines while modes 2, 3 and 4 detect which line segments are hidden and suppresses the drawing of these segments.

### *See Also* {#see-also}
[Waterfall Plots](/igorpro/graphing/graphs.md#waterfall-plots), [NewWaterfall](/igorpro/commands/newwaterfall.md), [ModifyGraph](/igorpro/commands/modifygraph.md)