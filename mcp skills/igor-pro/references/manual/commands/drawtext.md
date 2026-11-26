---
description: "The DrawText operation draws the specified text in the target graph, layout or control panel."
slug: /commands/drawtext
---

<div className="command-signature">

## <strong>DrawText</strong>  [/W=<em>winName</em> ] <em>x0</em>, <em>y0</em>, <em>textStr</em> {#drawtext}

</div>

The DrawText operation draws the specified text in the target graph, layout or control panel. The position of the text is determined by (*x*<sub>0</sub>, *y*<sub>0</sub>) along with the current *textxjust*, *textyjust* and *textrot* settings as set by [SetDrawEnv](/igorpro/commands/setdrawenv.md).

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Draws to the named window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
The coordinate system as well as the text's font, size, style and other properties are determined by the current drawing environment. The text is drawn in the current draw layer for the window, as determined by SetDrawLayer.

### *See Also* {#see-also}
[Drawing](/igorpro/graphing/drawing.md)

[SetDrawEnv](/igorpro/commands/setdrawenv.md), [SetDrawLayer](/igorpro/commands/setdrawlayer.md), [DrawAction](/igorpro/commands/drawaction.md)