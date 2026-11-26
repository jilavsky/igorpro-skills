---
description: "The DrawOval operation draws an oval in the target graph, layout or control panel within the rectangle defined by left, top, right and bottom."
slug: /commands/drawoval
---

<div className="command-signature">

## <strong>DrawOval</strong>  [/W=<em>winName</em> ] <em>left</em>, <em>top</em>, <em>right</em>, <em>bottom</em> {#drawoval}

</div>

The DrawOval operation draws an oval in the target graph, layout or control panel within the rectangle defined by *left*, *top*, *right* and *bottom*.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Draws to the named window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
The coordinate system as well as the oval's thickness, color and other properties are determined by the current drawing environment. The oval is drawn in the current draw layer for the window, as determined by SetDrawLayer.

### *See Also* {#see-also}
[Drawing](/igorpro/graphing/drawing.md)

[SetDrawEnv](/igorpro/commands/setdrawenv.md), [SetDrawLayer](/igorpro/commands/setdrawlayer.md), [DrawAction](/igorpro/commands/drawaction.md)