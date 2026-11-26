---
description: "The NewPanel operation creates a control panel window or subwindow, which may contain Igor controls and drawing objects."
slug: /commands/newpanel
---

<div className="command-signature">

## <strong>NewPanel</strong>  [ /EXP=<em>e</em> <em>EXT</em>=<em>e</em> /FG=(<em>gLeft</em>, <em>gTop</em>, <em>gRight</em>, <em>gBottom</em> )/FLT[=<em>f</em>  ] /HIDE=<em>h</em> /HOST=<em>hcSpec</em> /I /K=<em>k</em> /M/N=<em>name</em> /NA=<em>n</em> /W=(<em>left</em>, <em>top</em>, <em>right</em>, <em>bottom</em> ) ] [<em>as</em> <em>titleStr</em> ] {#newpanel}

</div>

The NewPanel operation creates a control panel window or subwindow, which may contain Igor controls and drawing objects.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/EXP = *e*</span> | Sets the expansion of the panel. *e* is a number between 0.25 to 8.0. Values of *e* greater than 1.0 make the panel, its controls, and its subwindows, appear larger than normal. |
|  | The expansion factor affects the size of the window specified by /W. |
|  | If you omit /EXP or specify /EXP=0, the expansion defaults to the value set in the Panel section of the Miscellaneous Settings dialog. |
|  | To change the expansion after the panel is created, use ModifyPanel expand=*e* or the Expansion submenu of the Panel menu. |
|  | The /EXP flag was added in Igor Pro 9.00. |
|  | See [Control Panel Expansion](/igorpro/user-interface/controls.md#control-panel-expansion) for further discussion. |
| <span class="table-cell-nowrap">/EXT = *e*</span> | Creates an exterior subwindow in combination with /HOST. e specifies the host window side location: |
|  |<table class="nested-table"><tbody><tr><td>*e*&nbsp;=0:</td><td>Right.</td></tr><tr><td>*e*&nbsp;=1:</td><td>Left.</td></tr><tr><td>*e*&nbsp;=2:</td><td>Bottom.</td></tr><tr><td>*e*&nbsp;=3:</td><td>Top.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/FG = (*gLeft*, *gTop*, *gRight*, *gBottom* )</span> |  |
|  | Specifies the frame guide to which the outer frame of the subwindow is attached inside the host window. |
|  | The standard frame guide names are FL, FR, FT, and FB for the left, right, top, and bottom frame guides, respectively, or user-defined guide names as defined by the host. Use * to specify a default guide name. |
|  | Guides may override the numeric positioning set by /W. |
| <span class="table-cell-nowrap">/FLT[ = *f* ]</span> | /FLT or /FLT=1 makes the panel a floating panel. |
|  | /FLT=2 makes it a floating panel with no close box. |
|  | /FLT=0 is the same as omitting /FLT and creates a regular (non-floating) control panel. |
|  | You must execute the following after the NewPanel command: |
|  | <code class="igor">SetActiveSubwindow \_endfloat\_</code> |
|  | ***See Floating Panels*** below for further information. |
| <span class="table-cell-nowrap">/FLTH = *h*</span> | Selects whether a floating panel is automatically hidden when Igor is deactivated. |
|  |<table class="nested-table"><tbody><tr><td>*h*=0:</td><td>The panel is not automatically hidden.</td></tr><tr><td>*h*=1:</td><td>The panel is automatically hidden.</td></tr></tbody></table>
|  | /FLTH was added in Igor Pro 9.00. |
|  | The default is platform specific and matches the behavior prior to Igor Pro 9. Floating panels are not hidden when Igor is deactivated. |
| <span class="table-cell-nowrap">/HIDE = *h*</span> | Hides (*h* = 1) or shows (*h* = 0, default) the window. |
| <span class="table-cell-nowrap">/HOST = *hcSpec*</span> | Embeds the new control panel in the host window or subwindow specified by *hcSpec*. |
|  | When identifying a subwindow with *hcSpec*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/I</span> | Sets coordinates to inches. |
| <span class="table-cell-nowrap">/K = *k*</span> | Specifies window behavior when the user attempts to close it. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills without dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr><tr><td>*k*&nbsp;=3:</td><td>Hides the window.</td></tr><tr><td>*k*&nbsp;=4:</td><td>Kills with no dialog and is not saved with the experiment.</td></tr></tbody></table>
|  | If you use /K=2 or /K=3, you can still kill the window using the [KillWindow](/igorpro/commands/killwindow.md) operation. |
|  | Exterior subwindows never display a dialog when killed. |
| <span class="table-cell-nowrap">/M</span> | Sets coordinates to centimeters. |
| <span class="table-cell-nowrap">/N = *name*</span> | Requests that the created panel have this name, if it is not in use. If it is in use, then *name*0, *name*1, etc are tried until an unused window name is found. In a function or macro, S_name is set to the chosen panel name. |
|  | Note that a function or macro with the same name will cause a name conflict. |
| <span class="table-cell-nowrap">/NA = *n*</span> | Sets panel no-activate mode. |
|  |<table class="nested-table"><tbody><tr><td>*n*&nbsp;=0:</td><td>Normal (default).</td></tr><tr><td>*n*&nbsp;=1:</td><td>Button click doesn&#39;t activate window but click outside of any control does.</td></tr><tr><td>*n*&nbsp;=2:</td><td>No activation even if click is outside controls. Title bar clicks still activate.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom*)</span> |  |
|  | Sets the initial coordinates of the panel window. See Interpretation of NewPanel Coordinates for a discussion of the *left*, *top*, *right*, and *bottom* parameters. |
|  | When used with the /HOST flag, the specified location coordinates can have one of two possible meanings: |
|  |<table class="nested-table"><tbody><tr><td>1.</td><td>When all values are less than 1, coordinates are assumed to be fractional relative to the host frame size. This applies to interior panels only, not to exterior panels.</td></tr><tr><td>2.</td><td>When any value is greater than 1, coordinates are taken to be fixed locations measured in points, or [control panel units](/igorpro/user-interface/controls.md#control-panel-units) for control panel hosts, relative to the top left corner of the host frame.</td></tr></tbody></table>
|  | When the subwindow position is fully specified using guides (using the /HOST or /FG flags), the /W flag may still be used although it is not needed. |

### *Details* {#details}
If /N is not used, NewPanel automatically assigns to the panel a window name of the form "Panel*n* ", where *n* is some integer. In a function or macro, the assigned name is stored in the S_name string. This is the name you can use to refer to the panel from a procedure. Use the [RenameWindow](/igorpro/commands/renamewindow.md) operation to rename the panel.

On Windows there are special considerations relating to screen resolution and control panels. See [Control Panel Resolution on Windows](/igorpro/user-interface/platform-related-issues.md#control-panel-resolution-on-windows) for details.

### *Floating Panels* {#floating-panels}
Floating control panels float above all other windows except dialogs. Because floating panels cover up other windows, you should use them sparingly and you should take care to make them small and unobtrusive.

Floating panels are not resizable by default. To allow panel resizing use


```igor
ModifyPanel fixedSize=0
```

Because floating panels always act as if they are on top, the standard rules for target windows and keyboard focus do not apply.

Normally, a floating panel is never the target window and control procedures will need to explicitly designate the target. But a newly-created floating panel is the default target and will remain so until you execute


```igor
SetActiveSubwindow _endfloat_
```

It also becomes the default target when the tools are showing and in any non-Operate mode. Similarly, a floating panel with tools not in Operate mode has keyboard focus. To avoid confusion, do not attempt to work on other windows when a floating panel is the default target.

When working with a floating panel, you can show or hide tools or create a recreation macro by right-clicking in the panel.

A floating panel does not have keyboard focus. However, a floating panel gains keyboard focus when a control that needs focus is clicked. Focus remains until you press Enter or Escape for a text entry in a setvariable, press Tab until no control has the focus, or until you click outside a focusable control.

If a floating panel has focus and you activate another window, the activate sequence will be fouled up leaving the windows in an indeterminate state. Consequently, it is important that you always finish any keyboard interaction started in a floating panel before moving on to other windows. If this can cause confusion, you should not use controls such as SetVariable and ListBox in a floating panel.

### *Exterior Subwindows* {#exterior-subwindows}
Exterior subwindows are automatically positioned along the designated side of a host window. The host window can be a graph, table, panel or Gizmo plot. You can designate fixed sizes or automatic size with minima. Subwindows are stacked beside the designated side in their creation order with the first one closest.

Subwindow dimensions have various meanings depending on their location. Interior values are taken to be additional grout, exterior values are taken to be sizes. For left or right panels, top is taken to be the minimum height and bottom, if not zero, is height. For top and bottom, left is taken to be the minimum width and right, if not zero, is width. Zero values default to 50 for width and height or size of host.

Exterior subwindows are nonresizable by default. Use ModifyPanel fixedSize=0 to allow manual resizing. If you resize a panel, the original window dimensions are lost. You can also use [MoveSubwindow](/igorpro/commands/movesubwindow.md) to resize the subwindow.

Unlike normal subwindows, exterior subwindows have a tools palette. Click in the window and then choose the Show Tools or Hide Tools menu item.

Exterior subwindows have hook functions independent of the host window.

### *Examples* {#examples}
In a new experiment, execute these commands on the command line to create two exterior subwindows:


```igor
Display
// Create panel on right with min height of 200 points, width of 100.
NewPanel/HOST=Graph0/EXT=0/W=(0,200,100,0)
// Create another panel on right with grout of 10 and height= width= 100.
NewPanel/HOST=Graph0/EXT=0/W=(10,0,100,100)
```

Now try resizing and moving the graph.

For a demonstration of how the various exterior panels work, copy the following code to the procedure window in a new experiment:


```igor
Function bpNewExSw(ba) : ButtonControl
	STRUCT WMButtonAction &ba

	switch( ba.eventCode )
		case 2: // mouse up
			ControlInfo/W=$ba.win ckUseRect
			Variable useR= V_Value
			ControlInfo/W=$ba.win popSide
			Variable side= V_Value-1
			ControlInfo/W=$ba.win ckResizeable
			Variable resizeable= V_Value
			WAVE w=root:epsizes
			if( useR )
				NewPanel/HOST=$ba.win/EXT=(side)/W=(w[0],w[1],w[2],w[3])
			else
				NewPanel/HOST=$ba.win/EXT=(side)
			endif
			if( resizeable )
				ModifyPanel fixedSize=0	// default is 1 for floating and exterior sw
			endif
			break
	endswitch

	return 0
End

Window ExSwTest() : Graph
	PauseUpdate; Silent 1		// building window...
	Display /W=(803,377,1158,591)
	Button bNewSW,pos={35,21},size={181,30},proc=bpNewExSw,title="New Exterior Subwindow"
	SetVariable svLeft,pos={118,82},size={96,15},title="left"
	SetVariable svLeft,limits={0,100,1},value= epsizes[0],bodyWidth= 76
	SetVariable svTop,pos={120,97},size={94,15},title="top"
	SetVariable svTop,limits={0,100,1},value= epsizes[1],bodyWidth= 76
	SetVariable svRight,pos={112,113},size={102,15},title="right"
	SetVariable svRight,limits={0,100,1},value= epsizes[2],bodyWidth= 76
	SetVariable svBottom,pos={103,129},size={111,15},title="bottom"
	SetVariable svBottom,limits={0,100,1},value= epsizes[3],bodyWidth= 76
	CheckBox ckUseRect,pos={70,62},size={61,14},title="Use Rect:",value= 0
	PopupMenu popSide,pos={73,149},size={78,20},title="Side"
	PopupMenu popSide,mode=1,popvalue="Right",value= #"\"Right;Left;Bottom;Top\""
	CheckBox ckResizeable,pos={76,176},size={65,14},title="Resizeable",value= 0
EndMacro

Function test()
	Make/O/N=4 epsizes=0
	Execute "ExSwTest()"
End
```

After compiling the procedures, execute `test()` on the command line. You can now experiment with different sides and size values.

### *See Also* {#see-also}
[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.

[Interpretation of NewPanel Coordinates](/igorpro/user-interface/controls.md#interpretation-of-newpanel-coordinates) for a discussion of the units used with NewPanel /W.

[ModifyPanel](/igorpro/commands/modifypanel.md)