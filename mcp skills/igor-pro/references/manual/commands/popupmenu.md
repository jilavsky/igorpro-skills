---
description: "The PopupMenu operation creates or modifies a pop-up menu control in the target or named window."
slug: /commands/popupmenu
---

<div className="command-signature">

## <strong>PopupMenu</strong>  [/Z] <em>ctrlName</em>  [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#popupmenu}

</div>

The PopupMenu operation creates or modifies a pop-up menu control in the target or named window.

For information about the state or status of the control, use the [ControlInfo](/igorpro/commands/controlinfo.md) operation.

### *Parameters* {#parameters}
*ctrlName* is the name of the PopupMenu control to be created or changed.

The following keyword=value parameters are supported:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">align = *alignment*</span> | Sets the alignment mode of the control. The alignment mode controls the interpretation of the *leftOrRight* parameter to the pos keyword. The align keyword was added in Igor Pro 8.00. |
|  | If *alignment*=0 (default), *leftOrRight* specifies the position of the left end of the control and the left end position remains fixed if the control size is changed. |
|  | If *alignment*=1, *leftOrRight* specifies the position of the right end of the control and the right end position remains fixed if the control size is changed. |
| <span class="table-cell-nowrap">appearance = {*kind* [, *platform* ]}</span> |  |
|  | Sets the appearance of the control. *platform* is optional. Both parameters are names, not strings. |
|  | *kind* can be one of `default`, `native`, or `os9`. |
|  | *platform* can be one of `Mac`, `Win`, or `All`. |
|  | See [Button](/igorpro/commands/button.md) and [DefaultGUIControls](/igorpro/commands/defaultguicontrols.md) for more appearance details. |
| <span class="table-cell-nowrap">bodyWidth = *width*</span> | Specifies an explicit size for the body (nontitle) portion of a PopupMenu control. By default (bodyWidth=0), the body portion autosizes depending on the current text. If you supply a bodyWidth>0, then the body is fixed at the size you specify regardless of the body text. This makes it easier to keep a set of controls right aligned when the default font is changed. |
| <span class="table-cell-nowrap">disable = *d*</span> | Sets user editability of the control. |
|  |<table class="nested-table"><tbody><tr><td>*d*=0:</td><td>Normal.</td></tr><tr><td>*d*=1:</td><td>Hide.</td></tr><tr><td>*d*=2:</td><td>Draw in gray state; disable control action.</td></tr></tbody></table>
| <span class="table-cell-nowrap">fColor = (*r*,*g*,*b*[,*a*])</span> | Sets the initial color of the title. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
|  | To further change the color of the title text, use escape sequences as described for title=*titleStr*. |
| <span class="table-cell-nowrap">focusRing = *fr*</span> | Enables or disables the drawing of a rectangle indicating keyboard focus: |
|  |<table class="nested-table"><tbody><tr><td>*fr*=0:</td><td>Focus rectangle will not be drawn.</td></tr><tr><td>*fr*=1:</td><td>Focus rectangle will be drawn (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">font = "*fontName*"</span> | Sets the font for the pop-up title. |
| <span class="table-cell-nowrap">fsize = *s*</span> | Sets the font size for the pop-up title. |
| <span class="table-cell-nowrap">fstyle = *fs*</span> | *fs* is a bitwise parameter with each bit controlling one aspect of the font style as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">guides = {*left, hcenter, right, top, vcenter, bottom*}</span> |  |
|  | Controls attachments of anchor points to layout guides. See [Laying Out Controls in Guides Mode](/igorpro/user-interface/controls.md#laying-out-controls-in-guides-mode) for detailed information and examples. |
|  | Each of *left, hcenter, right, top, vcenter, bottom* is replaced with the name of a layout guide of appropriate orientation. That is, *left, hcenter, right* indicate attachments to vertical guides, and *top, vcenter, bottom* indicate attachments to horizontal guides. Use the special name *kwNone* to represent an unattached anchor point. |
|  | An error results if you overconstrain a control's layout. Both the width and height of a [PopupMenu](/igorpro/commands/popupmenu.md) control are set by the title font and font size, the length of the title, and the *bodyWidth* keyword, if any. Consequently, only one anchor may be attached to layout guides in each direction, as attaching two anchor points would most likely result in an attempt to resize the checkbox control. |
|  | If you do not use the *bodyWidth* keyword, the total width of the control is affected by the width of the currently selected menu item, so if you want PopupMenu controls that align, you should use *bodyWidth*. |
|  | Using *kwNone* for all anchor points results in completely detaching a control from the layout guides. |
| <span class="table-cell-nowrap">help = {*helpStr* }</span> | Sets the help for the control. |
|  | *helpStr* is limited to 1970 bytes (255 in Igor Pro 8 and before). |
|  | You can insert a line break by putting "\r" in a quoted string. |
| <span class="table-cell-nowrap">mode = *m*</span> | Specifies the pop-up title location and selected menu item. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Title is in pop-up menu (no item is selected).</td></tr><tr><td>*m*&nbsp;&gt;0:</td><td>Title is to the left of pop-up menu, the selected menu item appears in the pop-up menu, and menu item number *m* is initially selected.</td></tr></tbody></table>
| noproc | Specifies that no procedure is to execute when the pop-up menu is clicked. |
| <span class="table-cell-nowrap">popColor = (*r*,*g*,*b*[,*a*])</span> | Specifies the color initially chosen in the color pop-up palette.  *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). See below for details. |
| <span class="table-cell-nowrap">popmatch = *matchStr*</span> | Sets mode to the enabled menu item that matches *matchStr*. *matchStr* may be a "wildcard" expression. See [stringmatch](/igorpro/commands/stringmatch.md). If no item is matched, mode is unchanged. |
| <span class="table-cell-nowrap">popvalue = *valueStr*</span> | Sets the string displayed by the menu when first created, if mode is not zero. See below for details. |
| <span class="table-cell-nowrap">pos = {*leftOrRight*,*top* }</span> | Sets the position in [control panel units](/igorpro/user-interface/controls.md#control-panel-units) of the top/left corner of the control if its alignment mode is 0 or the top/right corner of the control if its alignment mode is 1. See the align keyword above for details. |
| <span class="table-cell-nowrap">pos+ = {*dx,dy* }</span> | Offsets the position of the pop-up in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">proc = *procName*</span> | Specifies the procedure to execute when the pop-up menu is clicked. See *Pop-up Menu Action Procedure* below. |
| <span class="table-cell-nowrap">rename = *newName*</span> | Gives pop-up menu a new name. |
| <span class="table-cell-nowrap">size = {*width*,*height* }</span> | Sets size of the control in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">title = *titleStr*</span> | Sets title of pop-up menu to the specified string expression. Defaults to "" (no title). |
|  | Using escape codes you can change the font, size, style and color of the title. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details. |
| <span class="table-cell-nowrap">userdata(*UDName* ) = *UDStr*</span> |  |
|  | Sets the unnamed user data to *UDStr*. Use the optional (*UDName* ) to specify a named user data to create. You can retrieve the data using [GetUserData](/igorpro/commands/getuserdata.md). |
| <span class="table-cell-nowrap">userdata(*UDName* )+ = *UDStr*</span> |  |
|  | Appends *UDStr* to the current unnamed user data. Use the optional (*UDName* ) to append to the named user data. |
| <span class="table-cell-nowrap">value = *itemListSpec*</span> | Specifies the pop-up menu's items. *itemListSpec* can take several forms as described below under *Setting The Popup Menu Items*. |
| <span class="table-cell-nowrap">win = *winName*</span> | Specifies which window or subwindow contains the named control. If not given, then the top-most graph or panel window or subwindow is assumed. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The target window, or the window named with the win=winName keyword,  must be a graph or panel.

### *Pop-up Menu Action Procedure* {#pop-up-menu-action-procedure}
The action procedure for a pop-up menu control takes a predefined WMPopupAction structure as a parameter to the function:


```igor
Function PopupMenuAction(PU_Struct) : PopupMenuControl
	STRUCT WMPopupAction &PU_Struct
	...
	return 0
End
```

The ": PopupMenuControl" designation tells Igor to include this procedure in the list of available popup menu action procedures in the PopupMenu Control dialog.

See [WMPopupAction](/igorpro/programming/structures/wmpopupaction.md) for details on the WMPopupAction structure.

Although the return value is not currently used, action procedures should always return zero.

You may see an old format pop-up menu action procedure in old code:


```igor
Function PopupMenuAction (ctrlName,popNum,popStr) : PopupMenuControl
	String ctrlName
	Variable popNum	// which item is currently selected (1-based)
	String popStr		// contents of current popup item as string
	...
	return 0
End
```

This old format should not be used in new code.

### *Setting the Popup Menu Items* {#setting-the-popup-menu-items}
This section discusses popup menus containing lists of text items. The next section discusses popup menus for choosing colors, line styles, markers and patterns.

The items in the popup menu are determined by the *itemListSpec* parameter used with the value keyword. *itemListSpec* can take several different forms from simple to complex.

No matter what the form, Igor winds up storing an expression that returns a string in the popup menu's internal structure. This expression may be a literal string ("Red;Green;Blue;"), a call to a built-in or user-defined function that returns a string, or the path to a global string variable. Igor evaluates this expression when the popup menu is first created and again each time the user clicks on the menu. You can see the string expression for a given popup menu using the PopupMenu Control dialog.

The right form for *itemListSpec* depends on your application. Here is a guide to choosing the right form with the simpler forms first.

- ***A literal string expression***

	Use this if you know the items you want in your popup menu when you write the PopupMenu call. For example:


	```igor
	Function PopupDemo1()			// Literal string
		NewPanel
		PopupMenu popup0, value="Red;Green;Blue;"
	End
	```

	This method is limited to 2500 bytes of menu item text.

- ***A function call***

	Use this if you need to compute the popup menu item list when the user clicks the popup menu. The function must return a string containing a semicolon-separated list of menu items. This example creates a popup menu which displays the name of each wave in the current data folder at the time the menu is clicked:


	```igor
	Function PopupDemo2()			// Built-in function
		NewPanel
		PopupMenu popup0, value=WaveList("*", ";", "")
	End
	```

	You can also use a user-defined function. This example shows how to list waves from other than the current data folder:


	```igor
	Function/S MyPopupWaveList()
		// Create some waves for demo purposes
		DFREF saveDF = GetDataFolderDFR()
		NewDataFolder/O/S root:Packages
		NewDataFolder/O/S PopupMenuDemo
		Make/O demo0, demo1, demo2
		SetDataFolder saveDF

		DFREF saveDF = GetDataFolderDFR()
		SetDataFolder root:Packages:PopupMenuDemo
		String list = WaveList("*", ";", "")
		SetDataFolder saveDF
		
		return list
	End

	Function PopupDemo3()		// User-defined function
		NewPanel
		PopupMenu popup0, value=MyPopupWaveList()
	End
	```

- ***Followed by a local string variable specifying items***

	Use this when the popup menu item list is not known when you write the, code but you can compute it at runtime. For example:


	```igor
	Function PopupDemo4()		// Local string variable specifying items
		NewPanel
		String quote = "\""
		String list
		if (CmpStr(IgorInfo(2),"Windows") == 0)
			list = quote + "Windows XP; Windows VISTA;" + quote
		else
			list = quote + "Mac OS X 10.4;Mac OS X 10.5;" + quote
		endif
		PopupMenu popup0, value=#list
	End
	```

	The strange-looking use of the quote string variable is necessary because the parameter passed to the value=# keyword is evaluated once when the PopupMenu command executes and the result of that evaluation is evaluated again when the PopupMenu is created or clicked. The result of the first evaluation must be a legal string expression.

	This method is limited to 2500 bytes of menu item text.

- ***Followed by a local string variable specifying a function***

	Use this when you need to compute the popup menu item list at click time and you need to select the function which computes the list when the popup menu is created. For example:


	```igor
	Function/S WindowsItemList()
		String list
		list = "Windows XP; Windows VISTA;"
		return list
	End

	Function PopupDemo5()		// Local string variable specifying function
		String listFunc
		if (CmpStr(IgorInfo(2),"Windows") == 0)
			listFunc = "WindowsItemList()"
		else
			listFunc = "MacItemList()"
		endif
		NewPanel
		PopupMenu popup0, value=#listFunc
	End
	```

	This form is useful when you create a control panel in an independent module. Since the control panel runs in the global name space, you must specify the independent module name in the invocation of the function that provides the popup menu items. For example:


	```igor
	// Calling a non-static function in an independent module from #included code
	#pragma IndependentModuleName=IM
	. . .
	String listFunc= GetIndependentModuleName()+"#PublicFunctionInIndepMod()"
	PopupMenu popup0, value=#listFunc

	// Calling a static function in an independent module from #included code
	#pragma IndependentModuleName=IM
	#pragma ModuleName=ModName
	. . .
	String listFunc= GetIndependentModuleName()+"#ModName#StaticFunctionInIndepMod()"
	PopupMenu popup0, value=#listFunc
	```

	We use GetIndependentModuleName rather than hard-coding the name of the independent module so that the code will continue to work if the name of the independent module is changed. Also, because this code does not depend on the specific name of the independent module, it can be added to an independent module via a #included procedure file.

	Also see [GetIndependentModuleName](/igorpro/commands/getindependentmodulename.md) and [Independent Module Development Tips](/igorpro/advanced-topics.md#independent-module-development-tips).

- ***Followed by a quoted literal path to a global string variable***

	Use this if you want to compute the popup menu item list before it is clicked, not each time it is clicked. This would be advantageous if it takes a long time to compute the item list, and the list changes only at well-defined times when you can set the global string variable.

	The global string variable must exist when the PopupMenu command executes and when the menu is clicked. In this example, the gPopupMenuItems global string variable is created and initialized when the popup menu is created but can be changed to a different value later before the menu is clicked:


	```igor
	Function PopupDemo6()		// Global string variable containing list
		NewDataFolder/O root:Packages
		NewDataFolder/O root:Packages:PopupMenuDemo
		String/G root:Packages:PopupMenuDemo:gPopupMenuItems = "Red;Green;Blue;"	

		NewPanel
		PopupMenu popup0 ,value=#"root:Packages:PopupMenuDemo:gPopupMenuItems"
	End
	```

- ***Followed by a local string variable containing a path to a global string variable***

	Use this when the popup menu item list contents will be stored in a global string variable whose location is not known until the popup menu is created. For example:


	```igor
	Function PopupDemo7()		// Local string containing path to global string
		String graphName = WinName(0, 1, 1)	// Name of top graph
		if (strlen(graphName) == 0)
			Print "There are no graphs."
			return -1
		endif
		
		NewDataFolder/O root:Packages
		NewDataFolder/O root:Packages:PopupMenuDemo

		// Create data folder for graph
		NewDataFolder/O root:Packages:PopupMenuDemo:$(graphName)

		String list = "Red;Green;Blue;"
		String/G root:Packages:PopupMenuDemo:$(graphName):gPopupMenuItems = list
		
		NewPanel

		String path		// Local string containing path to global string
		path = "root:Packages:PopupMenuDemo:" + graphName + ":gPopupMenuItems"
		PopupMenu popup0, value=#path
		
		return 0
	End
	```

### *Colors, Color Tables, Line Styles, Markers and Patterns* {#colors-color-tables-line-styles-markers-and-patterns}
You can create PopupMenu controls for color, color tables, line style (dash modes), markers, and patterns. To do so, simply specify the *itemListSpec* parameter to the value keyword as one of `"*COLORPOP*"`, `"*COLORTABLEPOP*"`, `"*COLORTABLEPOPNONAMES*"`, `"*LINESTYLEPOP*"`, `"*MARKERPOP*"`, or `"*PATTERNPOP*"`. In these modes the body of the control will contain a color box, a color table (gradient), a line style sample, a marker, or a pattern sample.

For these special pop-up menus, mode=0 ("Title in Box" checked) is not used.

For a line style pop-up menu, the mode value is the line style number plus one. Thus line style 0 (a solid line) is mode=1.

For a marker pop-up, the mode value is the marker number plus one, and marker 0 (the + marker) is mode=1.

For a pattern pop-up, the mode value is the [SetDrawEnv](/igorpro/commands/setdrawenv.md) fillPat number minus 4, so mode=1 corresponds to fillpat=5, the SW-NE lines fill pattern shown above.

For a color table pop-up, the mode value is the CTabList() index plus 1, so mode=1 corresponds to the first item in the list returned by [CTabList](/igorpro/commands/ctablist.md), which is "Grays":


```igor
ControlInfo $ctrlName                       // Sets V_Value
Print StringFromList(V_Value-1,CTabList())  // Prints "Grays"
```

[ControlInfo](/igorpro/commands/controlinfo.md) also returns the color table name in S_Value.

To set the pop-up to a given color table name, you can use code like this:


```igor
Variable m = 1 + WhichListItem(ctabName, CTabList())
PopupMenu $ctrlName mode=m
```

For color pop-up menus, you set the current value using the popColor=(*r*,*g*,*b*[,*a*]) keyword. On output (via the popStr parameter of your action procedure or via the S_value from ControlInfo) the color is encoded as "(*r*,*g*,*b*)" or "(*r,g,b,a*)". To get these values numerically, you can extract them from the string using the MyRGBStrToRGB function below or use ControlInfo which sets V_Red, V_Green, V_Blue and V_Alpha. The following example demonstrates the line style and color pop-up menus. To run the example, copy the following code to the procedure window of a new experiment and then run the panel macro.


```igor
Window Panel0() : Panel
	PauseUpdate; Silent 1	// building window...
	NewPanel /W=(150,50,400,182)
	PopupMenu popup0,pos={74,31},size={96,20},proc=ColorPopMenuProc,title="colors"
	PopupMenu popup0,mode=1,popColor= (0,65535,65535),value= "*COLORPOP*"
	PopupMenu popup1,pos={9,68},size={221,20},proc=LStylePopMenuProc,title="line styles"
	PopupMenu popup1,mode=1,value= "*LINESTYLEPOP*"
EndMacro

Function ColorPopMenuProc(ctrlName,popNum,popStr) : PopupMenuControl
	String ctrlName
	Variable popNum
	String popStr
	
	Variable r,g,b,a
	MyRGBStrToRGB(popStr,r,g,b,a)	// One way to get r, g, b
	print popStr," gives: ",r,g,b,a

	ControlInfo $ctrlName	// Another way: Sets V_Red, V_Green, V_Blue, V_Alpha
	Printf "ControlInfo returned (%d,%d,%d,%d)\r", V_Red, V_Green, V_Blue, V_Alpha
	
	return 0
End

// Take (r,g,b, and possibly a) as a string and extract numeric r,g,b,a values
Function MyRGBStrToRGB(rgbStr,r,g,b,a)
	String rgbStr
	Variable &r, &g, &b, &a
	
	if (CmpStr(rgbStr[0], "(") == 0)
		rgbStr = rgbStr[1,inf]
	endif
	r = str2num(StringFromList(0, rgbStr, ","))
	g = str2num(StringFromList(1, rgbStr, ","))
	b = str2num(StringFromList(2, rgbStr, ","))
	a = 65535
	if (itemsinList(rgbStr) > 3)
		a = str2num(StringFromList(3, rgbStr, ","))
	endif
End

Function LStylePopMenuProc(ctrlName,popNum,popStr) : PopupMenuControl
	String ctrlName
	Variable popNum
	String popStr
	
	Print "style:",popNum-1
	
	return 0
End
```

### *Popvalue Keyword* {#popvalue-keyword}
There are times when the displayed value cannot be determined and saved such that it can be displayed when the pop-up menu is recreated. For instance, because window recreation macros are evaluated in the root folder, a pop-up menu of waves may not contain the correct list when a panel is recreated. That is, the intention may be to have the menu show a particular wave from a data folder other than root. When the panel recreation macro runs, the function that lists waves will list waves in the root data folder. The desired selection may be wrong or nonexistent.

Similarly, a pop-up menu of fonts may need to display a particular font upon recreation on a different computer having a different list of fonts. The mode=*m* keyword probably won't pick the correct font from the new list.

The solution to these problems is to save the correct selection with the popvalue=*valueStr* keyword. The list function will not be executed when the menu is first created. If the menu is popped, the list function will be evaluated, and the correct list will be displayed then.

It is a good idea to set the mode=*m* keyword to the correct number, if it is known. That way, when the menu is popped the correct item is selected.

Normally you can let Igor redraw the pop-up menu when it redraws the graph or control panel containing it. However, there are situations in which you may want to force the pop-up menu to be redrawn. This can be done using the [ControlUpdate](/igorpro/commands/controlupdate.md) operation.

### *See Also* {#see-also}
[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.

[Control Panel Units](/igorpro/user-interface/controls.md#control-panel-units) for a discussion of the units used for controls.

The [ControlInfo](/igorpro/commands/controlinfo.md) operation for information about the control.

The [GetUserData](/igorpro/commands/getuserdata.md) function for retrieving named user data.

The [ControlUpdate](/igorpro/commands/controlupdate.md), [WaveList](/igorpro/commands/wavelist.md), and [TraceNameList](/igorpro/commands/tracenamelist.md) operations.

[Special Characters in Menu Item Strings](/igorpro/user-interface/user-defined-menus.md#special-characters-in-menu-item-strings)