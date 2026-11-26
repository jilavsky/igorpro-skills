---
description: "The SetMarquee operation creates a marquee on the target graph or layout window or the specified window or subwindow."
slug: /commands/setmarquee
---

<div className="command-signature">

## <strong>SetMarquee</strong>  [/W=<em>winName</em> ] <em>left</em>, <em>top</em>, <em>right</em>, <em>bottom</em> {#setmarquee}

</div>

The SetMarquee operation creates a marquee on the target graph or layout window or the specified window or subwindow.

### *Parameters* {#parameters}
The *left*, *top*, *right*, and *bottom* coordinates are in units of points unless you specify /HAX or /VAX in which case they are in axis units. Axis units are allowed for graphs only, not for layouts.

If the coordinates are all 0, the marquee, if it exists, is killed.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/HAX = *hAxisName*</span> |  |
|  | Specifies that the *left* and *right* parameters are in units of the axis named by *hAxisName*. The /HAX flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/VAX = *vAxisName*</span> |  |
|  | Specifies that the *top* and *bottom* parameters are in units of the axis named by *vAxisName*. The /VAX flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Specifies the named window or subwindow. When omitted, action will affect the active window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
Igor stores marquee coordinates internally as integers in units of points. If you specify coordinates in axis units, there will be some roundoff error when Igor converts to integer points. This results in a small discrepancy between the coordinates you set using /HAX or /VAX and the coordinates returned by [GetMarquee](/igorpro/commands/getmarquee.md).

### *See Also* {#see-also}
[GetMarquee](/igorpro/commands/getmarquee.md)