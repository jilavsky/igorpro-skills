---
description: "The PopupContextualMenu operation displays a pop-up menu. The menu appears at the current mouse position or at the location specified by the /C flag."
slug: /commands/popupcontextualmenu
---

<div className="command-signature">

## <strong>PopupContextualMenu</strong>  [/C=(<em>xpix</em>, <em>ypix</em>) /N /ASYN[=<em>func</em>] ] <em>popupStr</em> {#popupcontextualmenu}

</div>

The PopupContextualMenu operation displays a pop-up menu.

The menu appears at the current mouse position or at the location specified by the /C flag.

The content of the menu is specified by *popupStr* as a semicolon-separated list of items or, if you include the /N flag, by a user-defined menu definition referred to by the name contained in *popupStr*.

If you omit the /ASYN flag, the menu is tracked and the operation does not return until the user makes a selection or cancels the menu by clicking outside of its window.

If you include /ASYN, the menu is displayed and the operation returns immediately. When the user makes a selection, then the result is sent to the specified function or to the user-defined menu's execution text. You can use /ASYN to allow a background task to continue while a contextual menu is popped up. /ASYN requires Igor Pro 7.00 or later.

### *Parameters* {#parameters}
If *popupStr* specifies the pop-up menu's items directly (/N is not specified), then *popupStr* is a semicolon-separated list of items such as "yes;no;maybe;", or a string expression that returns such a list, such as [TraceNameList](/igorpro/commands/tracenamelist.md).

The menu items can be formatted and checkmarked, like user-defined menus can. See [Special Characters in Menu Item Strings](/igorpro/user-interface/user-defined-menus.md#special-characters-in-menu-item-strings).

If /N is specified, *popupStr* must contain the name of a user-defined menu that also has the popupcontextualmenu keyword. See Example 3.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ASYN</span> | When used with /N: The user-defined menu is displayed and operation returns immediately. The result of menu selection is handled by the user-defined menu's execution text.  See [User-Defined Menus](/igorpro/user-interface/user-defined-menus.md). |
| <span class="table-cell-nowrap">/ASYN = *func*</span> | When used without /N: The user-defined menu is displayed and operation returns immediately. The result of menu selection or cancellation is handled by calling the named function, which must have the following format: |
|  | <code class="igor">Function func(String popupStr, String selectedText, Variable menuItemNum)</code> |
|  | In Igor Pro 8.05 and later, if the user cancels menu selection, selectedText will be "" and menuItemNum will be 0. |
| <span class="table-cell-nowrap">/C = (*xpix*, *ypix*)</span> | Sets the coordinates of the menu's top left corner. |
|  | Units are in pixels relative to the top-most window or the window specified by /W, like the MOUSEX and MOUSEY values passed to a window hook. See the window hook example, below and [SetWindow](/igorpro/commands/setwindow.md). |
|  | If /C is not specified, the menu's top left corner appears at the current mouse position. |
| <span class="table-cell-nowrap">/N</span> | Indicates that *popupStr* contains the name of a menu definition instead of containing a list of menu items. |
| <span class="table-cell-nowrap">/W = *winName*</span> | The /C coordinates are relative to the top left corner of the named window or subwindow. If you omit /W, /C uses the top-most window having focus. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
|  | /W was added in Igor Pro 7.00. |

### *Details* {#details}
PopupContextualMenu sets the following variables:

If you omit /N and /ASYN, PopupContextualMenu sets the following variables:


|  |  |
| --- | --- |
| V_flag | 0: User cancelled the menu without selecting an item, or there was an error such as an empty *popupStr*. |
|  | >= 1: 1 if the first menu item was selected, 2 for the second, etc. |
| S_selection | "" if the user cancelled or error, else the text of the selected menu item. |

If you include /N and omit /ASYN, PopupContextualMenu sets the following variables in a manner similar to [GetLastUserMenuInfo](/igorpro/commands/getlastusermenuinfo.md):


|  |  |
| --- | --- |
| V_kind | The kind of menu that was selected: |
|  |<table class="nested-table"><tbody><tr><td>**V_kind**</td><td>**Menu Kind**</td></tr><tr><td>0</td><td>Normal text menu item, including [Optional Menu Items](/igorpro/user-interface/user-defined-menus.md#optional-menu-items) and [Multiple Menu Items](/igorpro/user-interface/user-defined-menus.md#multiple-menu-items).</td></tr><tr><td>3</td><td>&quot;\*FONT\*&quot;</td></tr><tr><td>6</td><td>&quot;\*LINESTYLEPOP\*&quot;</td></tr><tr><td>7</td><td>&quot;\*PATTERNPOP\*&quot;</td></tr><tr><td>8</td><td>&quot;\*MARKERPOP\*&quot;</td></tr><tr><td>9</td><td>&quot;\*CHARACTER\*&quot;</td></tr><tr><td>10</td><td>&quot;\*COLORPOP\*&quot;</td></tr><tr><td>13</td><td>&quot;\*COLORTABLEPOP\*&quot;</td></tr></tbody></table>
|  | See [Specialized Menu Item Definitions](/igorpro/user-interface/user-defined-menus.md#specialized-menu-item-definitions) for details about these special user-defined menus. |
| V_flag | -1 if the user didn't select any item, otherwise V_flag returns a value which depends on the kind of menu the item was selected from: |
|  |<table class="nested-table"><tbody><tr><td>**V_kind**</td><td>**V_flag Meaning**</td></tr><tr><td>0</td><td>Text menu item number (the first menu item is number 1).</td></tr><tr><td>3</td><td>Font menu item number (use S_selection, instead).</td></tr><tr><td>6</td><td>Line style number (0 is solid line)</td></tr><tr><td>7</td><td>Pattern number (1 is the first selection, a SW-NE light diagonal).</td></tr><tr><td>8</td><td>Marker number (1 is the first selection, the X marker).</td></tr><tr><td>9</td><td>Character as an integer, = char2num(S_selection). Use S_selection instead.</td></tr><tr><td>10</td><td>Color menu item (use V_Red, V_Green, V_Blue and V_Alpha instead).</td></tr><tr><td>13</td><td>Color table list menu item (use S_selection instead).</td></tr></tbody></table>
| S_selection | The menu item text, depending on the kind of menu it was selected from: |
|  |<table class="nested-table"><tbody><tr><td>**V_kind**</td><td>**S_selection Meaning**</td></tr><tr><td>0</td><td>Text menu item text.</td></tr><tr><td>3</td><td>Font name or &quot;default&quot;.</td></tr><tr><td>6</td><td>Name of the line style menu or submenu.</td></tr><tr><td>7</td><td>Name of the pattern menu or submenu.</td></tr><tr><td>8</td><td>Name of the marker menu or submenu.</td></tr><tr><td>9</td><td>Character as string.</td></tr><tr><td>10</td><td>Name of the color menu or submenu.</td></tr><tr><td>13</td><td>Color table name.</td></tr></tbody></table>
|  | In the case of [Specialized Menu Item Definitions](/igorpro/user-interface/user-defined-menus.md#specialized-menu-item-definitions), S_selection will be the title of the menu or submenu, etc. |
| V_Red, V_Green, V_Blue, V_Alpha |  |
|  | If a user-defined color menu ("\*COLORPOP\*" menu item) was selected then these values hold the red, green, and blue values of the chosen color. The values range from 0 to 65535 - see [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
|  | Will be 0 if the last user-defined menu selection was not a color menu selection. |

If you include /N and /ASYN, PopupContextualMenu sets the following variables:

|  |  |
| --- | --- |
| V_flag |<table class="nested-table"><tbody><tr><td>0:</td><td>There was an error such as an empty *popupStr* or *popupStr* did not name a compiled user-defined menu.</td></tr><tr><td>-1</td><td>No error. The named user menu was valid and no item was selected yet.</td></tr></tbody></table>
| S_selection | "" |

If you include /ASYN and omit /N, PopupContextualMenu sets the following variables:


|  |  |
| --- | --- |
| V_flag |<table class="nested-table"><tbody><tr><td>0:</td><td>There was an error such as an empty *popupStr*.</td></tr><tr><td>-1:</td><td>No error. *popupStr* was valid and no item was selected yet.</td></tr></tbody></table>
| S_selection | "" |

### *Example 1 - popupStr contains a list of menu items* {#example-1-popupstr-contains-a-list-of-menu-items}

```igor
// Menu item formatting example:
String checked= "\\M0:!" + num2char(18) + ":" // checkmark code
String items= "first;\M1-;"+checked+"third;"  // 2nd is divider, 3rd is checked
PopupContextualMenu items
switch( V_flag )
	case 1:
		// do something because first item was chosen
		break;
	case 3:
		// do something because first item was chosen
		break;
endswitch
```

### *Example 2 - popupStr contains a list of menu items* {#example-2-popupstr-contains-a-list-of-menu-items}

```igor
// Window hook example:
SetWindow kwTopWin hook=TableHook, hookevents=1	// mouse down events
Function TableHook(infoStr)
	String infoStr
	String event= StringByKey("EVENT",infoStr)
	Print "EVENT= ",event
	strswitch(event)
		case "mousedown":
			Variable xpix= NumberByKey("MOUSEX",infoStr)
			Variable ypix= NumberByKey("MOUSEY",infoStr)
			PopupContextualMenu/C=(xpix, ypix) "yes;no;maybe;"
			strswitch(S_selection)
				case "yes":
					// do something because "yes" was chosen
					break;
				case "no":
					break;
				case "maybe":
					// do something because "maybe" was chosen
					break;
			endswitch
	endswitch
	return 0
End
```

### *Example 3 - popupStr contains the name of a user-defined menu* {#example-3-popupstr-contains-the-name-of-a-user-defined-menu}

```igor
// User-defined contextual menu example:
// dynamic menu (to keep WaveList items updated), otherwise not required.
// contextualmenu keyword is required, and implies /Q for all menu items.
//
// NOTE: Actions here are accomplished by the menu definition's 
// execution text, such as DoSomethingWithColor.
// See Example 4 for another approach.
//
Menu "ForContext", contextualmenu, dynamic
	"Hello", Beep
	Submenu "Color"
		"*COLORPOP*", DoSomethingWithColor()
	End
	Submenu "Waves"
		WaveList("*",";",""), /Q, DoSomethingWithWave()
	End
End

Function DoSomethingWithColor()
	GetLastUserMenuInfo
	Print V_Red, V_Green, V_Blue, V_Alpha
End
Function DoSomethingWithWave()
	GetLastUserMenuInfo
	WAVE w = $S_value
	Print "User selected "+GetWavesDataFolder(w,2)
End

// Use this code in a function or macro: 
PopupContextualMenu/N "ForContext"
if( V_flag < 0 )
	Print "User did not select anything"
endif
```

### *Example 4 - popupStr contains the name of a user-defined menu* {#example-4-popupstr-contains-the-name-of-a-user-defined-menu}

```igor
// User-defined contextual menu example:
Menu "JustColorPop", contextualmenu
	"*COLORPOP*(65535,0,0)", ;	// initially red, no execution command
End

// Use this code in a function or macro: 
PopupContextualMenu/C=(xpix, ypix)/N "JustColorPop"
if( V_flag < 0 )
	Print "User did not select anything"
else
	Print V_Red, V_Green, V_Blue, V_Alpha
endif
```

### *Example 5 - popupStr contains a list of menu items, asynchronous popup result* {#example-5-popupstr-contains-a-list-of-menu-items-asynchronous-popup-result}

```igor
Function YourFunction() 
	PopupContextualMenu/ASYN=Callback "first;second;third;"
	(YourFunction continues...)
End
// Routine called when/if popup menu item is selected. selectedItem=1 is the first item.
Function Callback(String list, String selectedText, Variable selectedItem)
	Print "Callback: ", list, selectedText, selectedItem
End
```

### *Example 6 - popupStr contains the name of a user-defined menu, asynchronous popup result* {#example-6-popupstr-contains-the-name-of-a-user-defined-menu-asynchronous-popup-result}

```igor
Function YourFunction() 
	PopupContextualMenu/ASYN/N "ForContext"
	(YourFunction continues...)
End
// Selection result is handled in "ForContext" menu's execution texts, as in Example 4
```

### *See Also* {#see-also}
[Creating a Contextual Menu](/igorpro/programming/interacting-with-the-user.md#creating-a-contextual-menu), [User-Defined Menus](/igorpro/user-interface/user-defined-menus.md)

[SetWindow](/igorpro/commands/setwindow.md), [Special Characters in Menu Item Strings](/igorpro/user-interface/user-defined-menus.md#special-characters-in-menu-item-strings), [PopupMenu](/igorpro/commands/popupmenu.md)

[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.