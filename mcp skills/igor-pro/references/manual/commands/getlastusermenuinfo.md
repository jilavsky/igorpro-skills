---
description: "The GetLastUserMenuInfo operation sets variables in the local scope to indicate the value of the last selected user-defined menu item."
slug: /commands/getlastusermenuinfo
---

<div className="command-signature">

## <strong>GetLastUserMenuInfo</strong> {#getlastusermenuinfo}

</div>

The GetLastUserMenuInfo operation sets variables in the local scope to indicate the value of the last selected user-defined menu item.

### *Details* {#details}
GetLastUserMenuInfo creates and sets these special variables:


|  |  |
| --- | --- |
| V_flag | The kind of menu that was selected: |
|  |<table class="nested-table"><tbody><tr><td>**V_flag**</td><td>**Menu Kind**</td></tr><tr><td>0</td><td>Normal text menu item, including [Optional Menu Items](/igorpro/user-interface/user-defined-menus.md#optional-menu-items) and [Multiple Menu Items](/igorpro/user-interface/user-defined-menus.md#multiple-menu-items).</td></tr><tr><td>3</td><td>&quot;\*FONT\*&quot;</td></tr><tr><td>6</td><td>&quot;\*LINESTYLEPOP\*&quot;</td></tr><tr><td>7</td><td>&quot;\*PATTERNPOP\*&quot;</td></tr><tr><td>8</td><td>&quot;\*MARKERPOP\*&quot;</td></tr><tr><td>9</td><td>&quot;\*CHARACTER\*&quot;</td></tr><tr><td>10</td><td>&quot;\*COLORPOP\*&quot;</td></tr><tr><td>13</td><td>&quot;\*COLORTABLEPOP\*&quot;</td></tr></tbody></table>
|  | See [Specialized Menu Item Definitions](/igorpro/user-interface/user-defined-menus.md#specialized-menu-item-definitions) for details about these special user-defined menus. |
| V_value | Which menu item was selected. The value also depends on the kind of menu the item was selected from: |
|  |<table class="nested-table"><tbody><tr><td>**V_flag**</td><td>**V_value meaning**</td></tr><tr><td>0</td><td>Text menu item number (the first menu item is number 1).</td></tr><tr><td>3</td><td>Font menu item number (use S_Value, instead).</td></tr><tr><td>6</td><td>Line style number (0 is solid line)</td></tr><tr><td>7</td><td>Pattern number (1 is the first selection, a SW-NE light diagonal).</td></tr><tr><td>8</td><td>Marker number (1 is the first selection, the X marker).</td></tr><tr><td>9</td><td>Character as an integer, = char2num(S_Value). Use S_Value instead.</td></tr><tr><td>10</td><td>Color menu item (use V_Red, V_Green, V_Blue and V_Alpha instead).</td></tr><tr><td>13</td><td>Color table list menu item (use S_Value instead).</td></tr></tbody></table>
| S_value | The menu item text, depending on the kind of menu it was selected from: |
|  |<table class="nested-table"><tbody><tr><td>**V_flag**</td><td>**S_value meaning**</td></tr><tr><td>0</td><td>Text menu item text.</td></tr><tr><td>3</td><td>Font name or &quot;default&quot;.</td></tr><tr><td>6</td><td>Name of the line style menu or submenu.</td></tr><tr><td>7</td><td>Name of the pattern menu or submenu.</td></tr><tr><td>8</td><td>Name of the marker menu or submenu.</td></tr><tr><td>9</td><td>Character as string.</td></tr><tr><td>10</td><td>Name of the color menu or submenu.</td></tr><tr><td>13</td><td>Color table name.</td></tr></tbody></table>
|  | In the case of [Specialized Menu Item Definitions](/igorpro/user-interface/user-defined-menus.md#specialized-menu-item-definitions), S_value will be the title of the menu or submenu, etc. |
| V_Red, V_Green, V_Blue, V_Alpha |  |
|  | If a user-defined color menu ("\*COLORPOP\*" menu item) was selected then these values hold the red, green, and blue values of the chosen color. The values range from 0 to 65535 - see [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
|  | These outputs are set to 0 if the last user-defined menu selection was not a color menu selection. |
| S_graphName, S_traceName, V_mouseX, V_mouseY |  |
|  | These variables are set only when the user chooses a user-defined menu item from the TracePopup, AllTracesPopup, or GraphPopup contextual menu. |
|  | S_graphName and S_traceName are initially "" until a user-defined menu selection is made from one of these contextual menus, and are not reset for each user-defined menu selection. |
|  | S_graphName is the full host-child specification for the graph. If the graph is embedded into a host window, S_graphName might be something like "Panel0#G0". See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax). |
|  | S_traceName is name of the trace that was selected by the trace contextual menu, or "" if the AllTracesPopup or GraphPopup menu was chosen. See [Trace Names](/igorpro/graphing/graphs.md#trace-names). |
|  | V_mouseX and V_mouseY, added in Igor Pro 8.00, are the mouse location of the click that invoked the contextual menu. The location is in pixels; use [AxisValFromPixel](/igorpro/commands/axisvalfrompixel.md) to determine the X and Y axis values that correspond to the pixel location. |
| S_tableName, S_firstColumnPath, S_columnName, V_mouseX, V_mouseY |  |
|  | Added in Igor Pro 9.00. |
|  | These variables are set only when the user chooses a user-defined menu item from the TablePopup contextual menu. |
|  | S_tableName,  S_firstColumnPath and S_columnName are initially "" until a user-defined menu selection is made from a TablePopup contextual menus, and are not reset for each user-defined menu selection. |
|  | S_tableName is the full host-child specification for the table. If the table is embedded into a host window, S_tableName might be something like "Panel0#T0". See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax). |
|  | S_firstColumnPath is full path to the wave selected by the table contextual menu, or "" if multiple columns from different waves were chosen. The full path is identical to [GetWavesDataFolder](/igorpro/commands/getwavesdatafolder.md)(wave,2). |
|  | S_columnName is name of the selected column as used in the [ModifyTable](/igorpro/commands/modifytable.md) command, or "" if multiple columns from different waves were selected. |
|  | You can obtain additional information about the selected cells in the table using the [GetSelection](/igorpro/commands/getselection.md) operation. |
|  | V_mouseX and V_mouseY are the mouse location of the click that invoked the contextual menu. The location is in pixels relative to the top-left corner of the table. |

### *Examples* {#examples}
A Multiple Menu Items menu definition:


```igor
Menu "Wave List", dynamic
	"Menu Item 1", <some command>
	"Menu Item 2", <some command>
	WaveList("*",";",""), DoSomethingWithWave()
End
```

The last item can create multiple menu items - one for each wave name returned by WaveList. If the user selects one of these items, the DoSomethingWithWave user function can call GetLastUserMenuInfo to determine which wave was selected:


```igor
Function DoSomethingWithWave()
	GetLastUserMenuInfo
	WAVE/Z selectedWave = $S_value
	// Use selectedWave for something
End
```

A trivial user-defined color menu definition:


```igor
Menu "Color"
	"*COLORPOP*", DoSomethingWithColor()
End

Function DoSomethingWithColor()
	GetLastUserMenuInfo
	// Do something with V_Red, V_Green, V_Blue, V_Alpha
End
```

See [Specialized Menu Item Definitions](/igorpro/user-interface/user-defined-menus.md#specialized-menu-item-definitions) for another color menu example.

A Trace contextual menu Items menu definition:


```igor
Menu "TracePopup", dynamic	// menu when a trace is right-clicked
	"-"					// separator divides this from built-in menu items
	ExportTraceName(), ExportSelectedTrace()
	"Draw XY Here", DrawXYHere()
End

Function/S ExportTraceName()
	GetLastUserMenuInfo	// Sets S_graphName, S_traceName, V_mouseX, V_mouseY 
	if (strlen(S_traceName) > 0)
		String item = "Export "+S_traceName
		return item
	endif
	return ""		// No item is added to menu
End

Function ExportSelectedTrace()
	GetLastUserMenuInfo
	// Do something with S_graphName, S_traceName
End

Function DrawXYHere()
	GetLastUserMenuInfo

	// Figure out mouse position within graph
	String info = traceinfo(S_graphName, S_traceName, 0)
	String xaxis = stringbykey("XAXIS",info)
	String yaxis = stringbykey("YAXIS",info)
	Variable x_pos = AxisValFromPixel(S_graphName, xaxis, V_mouseX)
	Variable y_pos = AxisValFromPixel(S_graphName, yaxis, V_mouseY)

	// Draw
	GetAxis/W=$S_graphName/Q $yaxis
	Variable miny=V_min, maxy=V_max
	GetAxis/W=$S_graphName/Q $xaxis
	Variable minx=V_min, maxx=V_max
	SetDrawLayer/W=$S_graphName/K userFront
	SetDrawEnv/W=$S_graphName push
	SetDrawEnv/W=$S_graphName xcoord=$xaxis, ycoord=$yaxis,save
	DrawLine/W=$S_graphName minx, y_pos, maxx, y_pos 	// horizontal line
	DrawLine/W=$S_graphName x_pos, miny, x_pos, maxy 	// vertical line
	SetDrawEnv/W=$S_graphName pop
End
```

### *See Also* {#see-also}
[User-Defined Menus](/igorpro/user-interface/user-defined-menus.md), [Optional Menu Items](/igorpro/user-interface/user-defined-menus.md#optional-menu-items), [Multiple Menu Items](/igorpro/user-interface/user-defined-menus.md#multiple-menu-items), [Specialized Menu Item Definitions](/igorpro/user-interface/user-defined-menus.md#specialized-menu-item-definitions)

[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)