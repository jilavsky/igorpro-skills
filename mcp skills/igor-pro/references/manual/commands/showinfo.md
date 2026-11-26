---
description: "The ShowInfo operation puts an information panel on the target or named graph."
slug: /commands/showinfo
---

<div className="command-signature">

## <strong>ShowInfo</strong>  [ /CP=<em>num</em> /W=<em>winName</em> ] {#showinfo}

</div>

The ShowInfo operation puts an information panel on the target or named graph. The information panel contains cursors and readouts of values associated with waves in the graph.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/CP = *num*</span> | Selects a cursor pair to display in the info panel. |
|  |<table class="nested-table"><tbody><tr><td>*num*&nbsp;=0:</td><td>Selects cursor A and cursor B.</td></tr><tr><td>*num*&nbsp;=1:</td><td>Selects cursor C and cursor D.</td></tr><tr><td>*num*&nbsp;=2:</td><td>Selects cursor E and cursor F.</td></tr><tr><td>*num*&nbsp;=3:</td><td>Selects cursor G and cursor H.</td></tr><tr><td>*num*&nbsp;=4:</td><td>Selects cursor I and cursor J.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/CP = {*n1*, *n2*, ...}</span> |  |
|  | Allows you to select multiple cursor pairs to be displayed in the info panel. The numbers *n1*, *n2*, etc., are the same as in the single-pair version of this flag. |
|  | This form of /CP was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/SIDE = *side*</span> | Selects the side of the host window where the info panel should be attached: |
|  |<table class="nested-table"><tbody><tr><td>*side*&nbsp;=&nbsp;0:</td><td>right side</td></tr><tr><td>*side*&nbsp;=&nbsp;1:</td><td>left side</td></tr><tr><td>*side*&nbsp;=&nbsp;2:</td><td>bottom side (default)</td></tr><tr><td>*side*&nbsp;=&nbsp;3:</td><td>top side</td></tr></tbody></table>
| <span class="table-cell-nowrap">/V = *num*</span> | If *num* is non-zero, selects a vertical layout for the info panel. Most appropriate when /SIDE=0 or 1. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Displays info panel in the named window. |

### *See Also* {#see-also}
[HideInfo](/igorpro/commands/hideinfo.md), [Info Panel and Cursors](/igorpro/graphing/graphs.md#info-panel-and-cursors), [Programming With Cursors](/igorpro/graphing/graphs.md#programming-with-cursors)