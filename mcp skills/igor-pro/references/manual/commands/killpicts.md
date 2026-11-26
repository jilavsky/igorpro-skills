---
description: "The KillPICTs operation removes one or more named pictures from the current Igor experiment."
slug: /commands/killpicts
---

<div className="command-signature">

## <strong>KillPICTs</strong>  [/A/Z] [<em>PICTName</em> [, <em>PICTName</em> ]...] {#killpicts}

</div>

The KillPICTs operation removes one or more named pictures from the current Igor experiment.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Kills all pictures in the experiment. |
| <span class="table-cell-nowrap">/Z</span> | Doesn't generate an error if a picture to be killed is in use or does not exist. To kill all pictures in the experiment, use KillPICTs/A/Z. |

### *Details* {#details}
You cannot kill a picture that is used in a graph or page layout.

:::warning
You ***can*** kill a picture that is referenced from a graph or layout recreation macro. If you do, the graph or layout cannot be completely recreated. Use the Find dialog (Edit menu) to locate a reference in the procedure window to a named picture you want to kill.
:::

### *See Also* {#see-also}
[Pictures](/igorpro/graphing/making-figures/graphics.md#pictures)