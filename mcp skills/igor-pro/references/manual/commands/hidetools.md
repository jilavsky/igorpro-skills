---
description: "The HideTools operation hides the tool palette in the top graph or control panel if it was previously shown by the ShowTools operation."
slug: /commands/hidetools
---

<div className="command-signature">

## <strong>HideTools</strong>   [/W=<em>winName</em> /A] {#hidetools}

</div>

The HideTools operation hides the tool palette in the top graph or control panel if it was previously shown by the ShowTools operation.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Size the window automatically to make extra room for the tool palette. This preserves the proportion and size of the actual graph area. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Hides the tool palette in the named window. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | *winName* must be either the name of a top-level window or a path leading to an exterior panel subwindow (see [Exterior Control Panels](/igorpro/user-interface/controls.md#exterior-control-panels)). |

### *See Also* {#see-also}
[ShowTools](/igorpro/commands/showtools.md)