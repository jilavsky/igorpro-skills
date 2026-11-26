---
description: "The AutoPositionWindow operation positions the window specified by windowName relative to the next lower window of the same kind or relative to the window…"
slug: /commands/autopositionwindow
---

<div className="command-signature">

## <strong>AutoPositionWindow</strong>  [/E][/M=<em>m</em> ][/R=<em>relWindow</em>] [<em>windowName</em>] {#autopositionwindow}

</div>

The AutoPositionWindow operation positions the window specified by *windowName* relative to the next lower window of the same kind or relative to the window given by the /R flag. If *windowName* is not specified, AutoPositionWindow acts on the target window.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/E</span> | Entire area of the monitor is used. Otherwise, provision is made for the command window. |
| <span class="table-cell-nowrap">/M = *m*</span> | Specifies the positioning method. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Positions *windowName* to the right of the other window, if possible. If there is no room, then *windowName* is positioned just below the other window but at the left edge of the display area. If that is not possible, then the position is not affected.</td></tr><tr><td>*m*&nbsp;=1:</td><td>Positions *windowName* just under the other window lined up on the left edge, if possible. If there is no room, then *windowName* is positioned just to the right of the other window lined up on the bottom edges. If neither are possible then positions *windowName* as far to the bottom and right as it will go.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/R = *relWindow*</span> | Positions *windowName* relative to *relWindow*. |