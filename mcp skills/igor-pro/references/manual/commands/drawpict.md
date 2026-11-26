---
description: "The DrawPICT operation draws the named picture in the target graph, layout or control panel."
slug: /commands/drawpict
---

<div className="command-signature">

## <strong>DrawPICT</strong>  [/W=<em>winName</em> ][/RABS ] <em>left</em>, <em>top</em>, <em>hScaling</em>, <em>vScaling</em>, <em>pictName</em> {#drawpict}

</div>

The DrawPICT operation draws the named picture in the target graph, layout or control panel. The *left* and *top* parameters set the position of the top/left corner of the picture. *hScaling* and *vScaling* set the horizontal and vertical scale factors with 1 meaning 100%.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/RABS</span> | Draws the named picture using absolute scaling. In this mode, the picture is drawn in the rectangle defined by *left* and *top* for point (x<sub>0</sub>,y<sub>0</sub>), and by *hScaling* and *vScaling* for point (x<sub>1</sub>,y<sub>1</sub>), respectively. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Draws to the named window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
The coordinate system for the left and top parameters is determined by the current drawing environment. The picture is drawn in the current draw layer for the window, as determined by SetDrawLayer.

### *See Also* {#see-also}
[Drawing](/igorpro/graphing/drawing.md)

[SetDrawEnv](/igorpro/commands/setdrawenv.md), [SetDrawLayer](/igorpro/commands/setdrawlayer.md) [DrawAction](/igorpro/commands/drawaction.md)