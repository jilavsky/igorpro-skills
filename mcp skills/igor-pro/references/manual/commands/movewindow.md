---
description: "The MoveWindow operation moves the target or specified window to the given coordinates."
slug: /commands/movewindow
---

<div className="command-signature">

## <strong>MoveWindow</strong>  [/C/F/I/M/P=<em>procedureTitleAsName</em> /W=<em>winName</em>] <em>left</em>, <em>top</em>, <em>right</em>, <em>bottom</em> {#movewindow}

</div>

The MoveWindow operation moves the target or specified window to the given coordinates.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C</span> | Moves command window. |
| <span class="table-cell-nowrap">/F</span> | Moves the Igor application "frame". The frame is then adjusted so that no part of it is offscreen. |
| <span class="table-cell-nowrap">/I</span> | Coordinates are in inches. |
| <span class="table-cell-nowrap">/M</span> | Coordinates are in centimeters. |
| <span class="table-cell-nowrap">/P = *procedureTitleAsName*</span> |  |
|  | Moves the specified procedure window. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Moves the named window. |

### *Details* {#details}
Note that neither *winName* nor *procedureTitleAsName* is a string but is the actual window name or procedure window title. If the procedure window's title (procedure windows don't have names) has a space in it, use $ and quotes:


```igor
MoveWindow/P=$"Log Histogram" 0,0,600,400
```

If /W, /C, /F and /P are omitted, MoveWindow moves the target window.

The coordinates are in points if neither /I nor /M is used.

In Igor Pro 7.00 or later, to move the window without changing its size, pass -1 for both *right* and *bottom*.

You can use the MoveWindow operation to minimize, restore, or maximize a window by specifying 0, 1, or 2 for all of the coordinates, as follows:


```igor
MoveWindow 0, 0, 0, 0	// Minimize target window.
MoveWindow 1, 1, 1, 1	// Restore target window.
MoveWindow 2, 2, 2, 2	// Maximize target window.
```

If the window size has been constrained by [SetWindow](/igorpro/commands/setwindow.md) sizeLimit, those limits are silently applied to the size set by MoveWindow.

### *See Also* {#see-also}
[DoWindow](/igorpro/commands/dowindow.md), [MoveSubwindow](/igorpro/commands/movesubwindow.md)