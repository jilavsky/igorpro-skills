---
description: "The TileWindows operation tiles the specified windows in the Igor frame window."
slug: /commands/tilewindows
---

<div className="command-signature">

## <strong>TileWindows</strong>  [<em>flags</em>] [<em>windowName</em> [, <em>windowName</em> ]...] {#tilewindows}

</div>

The TileWindows operation tiles the specified windows in the Igor frame window.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = (*rows*,*cols* )</span> | Specifies number of rows/columns in which to tile windows. |
| <span class="table-cell-nowrap">/C</span> | Adds the command window to the windows to be tiled. |
| <span class="table-cell-nowrap">/G = *grout*</span> | Specifies grout, the spacing between tiles, in prevailing units (points unless /I or /M are used). |
| <span class="table-cell-nowrap">/I</span> | Specifies coordinates measured in inches. |
| <span class="table-cell-nowrap">/M</span> | Specifies coordinates measured in centimeters. |
| <span class="table-cell-nowrap">/O = *objTypes*</span> | Adds windows of types specified by *objTypes* to windows to be tiled. *objTypes* is a bitwise mask where: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Graphs</td></tr><tr><td>Bit&nbsp;1:</td><td>Tables</td></tr><tr><td>Bit&nbsp;2:</td><td>Page layouts</td></tr><tr><td>Bit&nbsp;4:</td><td>Notebooks</td></tr><tr><td>Bit&nbsp;6:</td><td>Control panels</td></tr><tr><td>Bit&nbsp;7:</td><td>Procedure windows</td></tr><tr><td>Bit&nbsp;9:</td><td>Help windows</td></tr><tr><td>Bit&nbsp;12:</td><td>XOP target windows</td></tr><tr><td>Bit&nbsp;14:</td><td>Camera windows</td></tr><tr><td>Bit&nbsp;16:</td><td>Gizmo windows</td></tr></tbody></table>
|  | Other bits should always be zero. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">/P</span> | Adds the main procedure window to the windows to be tiled. |
| <span class="table-cell-nowrap">/R</span> | Specifies coordinates measured in % of tiling rectangle. |
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom* )</span> |  |
|  | Specifies tiling rectangle on the screen. Coordinates are in points unless /I, /M, or /R are specified before /W. |
| <span class="table-cell-nowrap">/WINS = *windowListStr*</span> | Specifies the windows to be tiled using a semicolon-separated list of window names. Added in Igor Pro 9.00. |

### *Details* {#details}
If you omit the /W flag, the default tiling area is used. This is the area above your preferred command window position. You can set this using Misc→Command Buffer→Capture Prefs or Misc→History Area→Capture Prefs.

The windows to be tiled are determined by the /WINS, /C, /P and /O=*objTypes* flags and by the *windowNames*. If none of these flags are present and there are no *windowNames* then all windows are tiled.

Otherwise the windows to be tiled are determined as follows:

-	All visible named windows are tiled.
-	All visible windows specified by /WINS are tiled.
-	If the /C flag is present and the command window is visible, the command window is also tiled.
-	If the /P flag is present and the procedure window is visible, the procedure window is also tiled.
-	If the /O=*objTypes* flag is present then any visible windows specified by *objTypes* are also tiled.

### *Examples* {#examples}
To tile all the visible procedure windows, including the main one, use:


```igor
TileWindows/P/O=128	// 27=128
```

### *See Also* {#see-also}
[StackWindows](/igorpro/commands/stackwindows.md)