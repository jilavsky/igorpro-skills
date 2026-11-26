---
description: "The ShowTools operation puts a tool palette for drawing along the left hand side of the target or named graph or control panel, and optionally activates the…"
slug: /commands/showtools
---

<div className="command-signature">

## <strong>ShowTools</strong>   [/W=<em>winName</em> /A] [ <em>toolName</em> ] {#showtools}

</div>

The ShowTools operation puts a tool palette for drawing along the left hand side of the target or named graph or control panel, and optionally activates the named tool.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Automatically size the window to make extra room for the tool palette. This preserves the proportion and size of the actual graph area. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Shows the tool palette in the named window. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | *winName* must be either the name of a top-level window or a path leading to an exterior panel subwindow (see [Exterior Control Panels](/igorpro/user-interface/controls.md#exterior-control-panels)). |

### *Parameters* {#parameters}
If you specify a *toolName* (which can be one of: normal, guides, arrow, text, line, rect, rrect, oval,  poly, or usershape) the named tool is activated. Specifying the "normal" tool has the same effect as issuing the [GraphNormal](/igorpro/commands/graphnormal.md) command for a graph that has the drawing tools selected.

### *Details* {#details}
The activated tool is not highlighted until the top graph or control panel becomes the topmost (activated) window. Use [DoWindow](/igorpro/commands/dowindow.md)/F to bring a window to the top (or "front").

### *See Also* {#see-also}
[DoWindow](/igorpro/commands/dowindow.md), [GraphNormal](/igorpro/commands/graphnormal.md), [GraphWaveDraw](/igorpro/commands/graphwavedraw.md), [GraphWaveEdit](/igorpro/commands/graphwaveedit.md), [HideTools](/igorpro/commands/hidetools.md)