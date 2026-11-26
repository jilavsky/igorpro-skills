---
description: "The KillControl operation kills the named control in the top or specified graph or panel window or subwindow."
slug: /commands/killcontrol
---

<div className="command-signature">

## <strong>KillControl</strong>  [/W=<em>winName</em> ] <em>controlName</em> {#killcontrol}

</div>

The KillControl operation kills the named control in the top or specified graph or panel window or subwindow.

If the named control does not exist, KillControl does not complain.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Looks for the control in the named graph or panel window or subwindow. If /W is omitted, KillControl looks in the top graph or panel window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |