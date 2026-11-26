---
description: "The Tile operation tiles the specified objects in the top page layout."
slug: /commands/tile
---

<div className="command-signature">

## <strong>Tile</strong>  [/A=(<em>rows</em>,<em>cols</em>) /BBOX[=<em>ubb</em>] /G=<em>grout</em>  /I /M /O=<em>objTypes</em> /PA[=<em>preserve</em>] /R /S/W=(<em>left</em>,<em>top</em>,<em>right</em>,<em>bottom</em>)] [<em>objectName</em> [, <em>objectName</em> ]...] {#tile}

</div>

The Tile operation tiles the specified objects in the top page layout.

### *Parameters* {#parameters}
*objectName* is the name of a graph, table, picture or annotation object in the top page layout.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = (*rows*,*cols*)</span> | Specifies number of rows/columns in which to tile objects. |
| <span class="table-cell-nowrap">/BBOX[ = *ubb*]</span> | Specifies that you want to use the bounding box of the objects to be tiled as the tiling area. /BBOX overrides /W. See [Specifying the Tiling Area](/igorpro/graphing/making-figures/page-layouts.md#specifying-the-tiling-area) for details. Added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/G = *grout*</span> | Specifies grout, the spacing between tiles, in prevailing coordinates (points unless preceded by /I, /M or /R). |
| <span class="table-cell-nowrap">/I</span> | Specifies coordinates in inches. |
| <span class="table-cell-nowrap">/M</span> | Specifies coordinates in centimeters. |
| <span class="table-cell-nowrap">/O = *objTypes*</span> | Adds objects of type(s) specified by bitwise mask to list of objects to be tiled: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Tile graphs.</td></tr><tr><td>Bit&nbsp;1:</td><td>Tile tables.</td></tr><tr><td>Bit&nbsp;3:</td><td>Tile pictures.</td></tr><tr><td>Bit&nbsp;5:</td><td>Tile textboxes.</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">/PA[ = *preserve*]</span> | /PA and /PA=1 specify that you want to preserve the rough arrangement of the objects to be tiled. See [Preserving Your Rough Arrangement](/igorpro/graphing/making-figures/page-layouts.md#preserving-your-rough-arrangement) for details. Added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/R</span> | Specifies coordinates measured in percent of the printable page. |
| <span class="table-cell-nowrap">/S</span> | Adds selected objects to objects to be tiled. |
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom*)</span> |  |
|  | Specifies area in page layout in which to tile objects. Coordinates for /W are in points unless /I, /M or /R are specified before /W. /BBOX overrides /W. |

### *Details* {#details}
If /A=(*rows*,*cols*) is not used, Tile uses an appropriate number of rows and columns.

If /A=(*rows*,*cols*) is used, objects are tiled in a grid of that many rows and columns.

If *rows* or *cols* is zero, it substitutes an appropriate number for the zero parameter.

The objects to be tiled are determined by the /S and /O=*objTypes* flags and by any *objectName*s.

If no /S or /O flags are present and there are no *objectNames*, then all objects in the layout are tiled.

Otherwise the objects to be tiled are determined as follows:

-	All objects specified by *objectNames* are tiled.
-	If the /S flag is present, the selected objects, if any, are also tiled.
-	If the /O=*objTypes* flag is present then any objects specified by *objTypes* are also tiled. *objTypes* is a bitwise mask, so /O=3 tiles both graphs and tables.

### *See Also* {#see-also}
[Stack](/igorpro/commands/stack.md)