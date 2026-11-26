---
description: "The DrawRect operation draws a rectangle in the target graph, layout or control panel within the rectangle defined by left, top, right, and bottom."
slug: /commands/drawrect
---

<div className="command-signature">

## <strong>DrawRect</strong>  [/W=<em>winName</em> ] <em>left</em>, <em>top</em>, <em>right</em>, <em>bottom</em> {#drawrect}

</div>

The DrawRect operation draws a rectangle in the target graph, layout or control panel within the rectangle defined by *left*, *top*, *right*, and *bottom*.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Draws to the named window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
The coordinate system as well as the rectangle's thickness, color, dash pattern and other properties are determined by the current drawing environment. The rectangle is drawn in the current draw layer for the window, as determined by SetDrawLayer.

### *See Also* {#see-also}
[Drawing](/igorpro/graphing/drawing.md)

[SetDrawEnv](/igorpro/commands/setdrawenv.md), [SetDrawLayer](/igorpro/commands/setdrawlayer.md), [DrawAction](/igorpro/commands/drawaction.md)