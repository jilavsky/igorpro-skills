---
description: "The DrawLine operation draws a line in the target graph, layout or control panel from (x0,y0) to (x1,y1)."
slug: /commands/drawline
---

<div className="command-signature">

## <strong>DrawLine</strong>  [/W=<em>winName</em> ] <em>x0</em>, <em>y0</em>, <em>x1</em>, <em>y1</em> {#drawline}

</div>

The DrawLine operation draws a line in the target graph, layout or control panel from (*x*<sub>0</sub>,*y*<sub>0 </sub>) to (*x*<sub>1</sub>,*y*<sub>1 </sub>).

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Draws to the named window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
The coordinate system as well as the line's thickness, color, dash pattern and other properties are determined by the current drawing environment. The line is drawn in the current draw layer for the window, as determined by SetDrawLayer.

### *See Also* {#see-also}
[Drawing](/igorpro/graphing/drawing.md)

[SetDrawEnv](/igorpro/commands/setdrawenv.md), [SetDrawLayer](/igorpro/commands/setdrawlayer.md), [DrawAction](/igorpro/commands/drawaction.md)