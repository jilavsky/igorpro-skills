---
description: "The TabControl operation creates tab panels for controls. For information about the state or status of the control, use the ControlInfo operation."
slug: /commands/tabcontrol
---

<div className="command-signature">

## <strong>TabControl</strong>  [/Z] <em>ctrlName</em>  [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#tabcontrol}

</div>

The TabControl operation creates tab panels for controls.

For information about the state or status of the control, use the ControlInfo operation.

### *Parameters* {#parameters}
*ctrlName* is the name of the TabControl to be created or changed.

The following keyword=value parameters are supported:

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">align = *alignment*</span> | Sets the alignment mode of the control. The alignment mode controls the interpretation of the *leftOrRight* parameter to the pos keyword. The *align* keyword was added in Igor Pro 8.00. |
|  | If *alignment*=0 (default), *leftOrRight* specifies the position of the left end of the control and the left end position remains fixed if the control size is changed. |
|  | If *alignment*=1, *leftOrRight* specifies the position of the right end of the control and the right end position remains fixed if the control size is changed. |
| <span class="table-cell-nowrap">appearance = {*kind*  [, *platform* ]}</span> |  |
|  | Sets the appearance of the control. *platform* is optional. Both parameters are names, not strings. |
|  | *kind*  can be one of `default`, `native`, or `os9`. |
|  | *platform*  can be one of `Mac`, `Win`, or `All`. |
|  | See [DefaultGUIControls](/igorpro/commands/defaultguicontrols.md) ***TabControl Background Details*** for how enclosed controls are affected by native TabControl appearance. |
|  | See [Button](/igorpro/commands/button.md) for more appearance details. |
| <span class="table-cell-nowrap">disable = *d*</span> | Sets user editability of the control. |
|  |<table class="nested-table"><tbody><tr><td>*d*&nbsp;=0:</td><td>Normal.</td></tr><tr><td>*d*&nbsp;=1:</td><td>Hide.</td></tr><tr><td>*d*&nbsp;=2:</td><td>Draw in gray state; disable control action.</td></tr></tbody></table>
| <span class="table-cell-nowrap">fColor = (*r*,*g*,*b*[,*a*])</span> | Sets the initial color of the tab labels. *r*, *g*, *b*, and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). Use of transparency is discouraged. The default is opaque black. |
|  | To further change the color of the tab labels text, use escape sequences in the text specified by the tabLabel keyword. |
| <span class="table-cell-nowrap">focusRing = *fr*</span> | Enables or disables the drawing of a rectangle indicating keyboard focus: |
|  |<table class="nested-table"><tbody><tr><td>*fr*=0:</td><td>Focus rectangle will not be drawn.</td></tr><tr><td>*fr*=1:</td><td>Focus rectangle will be drawn (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">font = "*fontName*"</span> | Sets font for tabs. |
| <span class="table-cell-nowrap">fsize = *s*</span> | Sets font size for tabs. |
| <span class="table-cell-nowrap">fstyle = *fs*</span> | *fs* is a bitwise parameter with each bit controlling one aspect of the font style as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">guides = {*left*, *hcenter*, *right*, *top*, *vcenter*, *bottom*}</span> |  |
|  | Controls attachments of anchor points to layout guides. See [Laying Out Controls in Guides Mode](/igorpro/user-interface/controls.md#laying-out-controls-in-guides-mode) for detailed information and examples. |
|  | Each of *left*, *hcenter*, *right*, *top*, *vcenter*, *bottom* is replaced with the name of a layout guide of appropriate orientation. That is, *left*, *hcenter*, *right* indicate attachments to vertical guides, and *top*, *vcenter*, *bottom* indicate attachments to horizontal guides. Use the special name *kwNone* to represent an unattached anchor point. |
|  | An error results if you overconstrain a control's layout. Of the three horizontal or vertical anchor points, at most two may be attached to layout guides. Attaching one of the three causes a control to move as the layout guide moves. Attaching two causes a control to both move and resize. Because of limits on constraints, the name *kwNone* will appear at least twice. |
|  | Using *kwNone* for all anchor points results in completely detaching a control from the layout guides.
| <span class="table-cell-nowrap">help = {*helpStr*}</span> | Sets the help for the control. |
|  | *helpStr* is limited to 1970 bytes (255 in Igor Pro 8 and before). |
|  | You can insert a line break by putting "\\r" in a quoted string. |
| <span class="table-cell-nowrap">labelBack = (*r*,*g*,*b*[,*a*]) or 0</span> |  |
|  | Sets fill color for current tab and the interior. r, g, b, and a specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The actual result may be platform dependent. |
|  | If not set, then interior is transparent and the current tab is filled with the window background, though this style is platform-dependent. |
|  | If an opaque fill color is used, drawing objects will not be seen because they will be covered up. |
| noproc | Specifies that no function is to run when tab is pressed. |
| <span class="table-cell-nowrap">pos = {*leftOrRight*,*top*}</span> | Sets the position in [control panel units](/igorpro/user-interface/controls.md#control-panel-units) of the top/left corner of the control if its alignment mode is 0 or the top/right corner of the control if its alignment mode is 1. See the *align* keyword above for details. |
| <span class="table-cell-nowrap">pos+ = {*dx*,*dy*}</span> | Offsets the position of the control in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">proc = *procName*</span> | Specifies the function to run when the tab is pressed. It is the job of your function to hide and show other controls as desired. The TabControl does not do this automatically. |
| <span class="table-cell-nowrap">rename = *newName*</span> | Gives the control a new name. |
| <span class="table-cell-nowrap">size = {*width*,*height*}</span> | Sets TabControl size in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">tabLabel(*n*) = *lbl*</span> | Sets *n*th tab label to *lbl*. |
|  | Set the label of the last tab to "" to remove the last tab. |
|  | Using escape codes you can change the font, size, style and color of the label. See Annotation Escape Codes for details. |
| <span class="table-cell-nowrap">userdata(*UDName*) = *UDStr*</span> |  |
|  | Sets the unnamed user data to *UDStr*. Use the optional (*UDName*) to specify a named user data to create. |
| <span class="table-cell-nowrap">userdata(*UDName*)+ = *UDStr*</span> |  |
|  | Appends UDStr  to the current unnamed user data. Use the optional (*UDName*) to append to the named user data. |
| <span class="table-cell-nowrap">value = *v*</span> | Sets current tab number. Tabs count from 0. |
| <span class="table-cell-nowrap">win = *winName*</span> | Specifies which window or subwindow contains the named control. If not given, then the top-most graph or panel window or subwindow is assumed. |
|  | When identifying a subwindow with winName, see Subwindow Syntax for details on forming the window hierarchy. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}

The target window must be a graph or panel.

### *Tab Control Action Procedure* {#tab-control-action-procedure}

The action procedure for a TabControl takes a predefined WMTabControlAction structure as a parameter to the function:

```igor
Function ActionProcName(TC_Struct) : TabControl
	STRUCT WMTabControlAction &TC_Struct
	...
	return 0
End
```

The ": TabControl" designation tells Igor to include this procedure in the Procedure pop-up menu in the Tab Control dialog.

See [WMTabControlAction](/igorpro/programming/structures/wmtabcontrolaction.md) for details on the WMTabControlAction structure.

Although the return value is not currently used, action procedures should always return zero.

When clicking a TabControl with the selector arrow, click in the title region. The control is not selected if you click in the body. This is to make it easier to select controls in the body rather than the TabControl itself.

### *Example* {#example}

Designing a TabControl with all the accompanying interior controls can be somewhat difficult. Here is a suggested technique:

First, create and set the size and label for one tab. Then create the various controls for this first tab. Before starting on the second tab, create the TabControl's procedure so that it can be used to hide the first set of controls. Then add the second tab, click it to run your procedure and start adding controls for this new tab. When done, update your procedure so the new controls are hidden when you start on the third tab. 

Here is an example:

1. Create a panel and a TabControl:

```igor
NewPanel /W=(150,50,478,250)
ShowTools
TabControl MyTabControl,pos={29,38},size={241,142},tabLabel(0)="First Tab",value= 0
```

2. Add a few controls to the interior of the TabControl:

```igor
Button button0,pos={52,72},size={80,20},title="First"
CheckBox check0,pos={52,105},size={102,15},title="Check first",value= 0
```

3. Write an action procedure:

```igor
Function TabActionProc(tc) : TabControl
	STRUCT WMTabControlAction& tc
	
	switch (tc.eventCode)
		case 2:			// Mouse up
			Button button0, disable=(tc.tab!=0)
			CheckBox check0, disable=(tc.tab!=0)
			break
	endswitch
	
	return 0
End
```

4. Set the action procedure and add a new tab:

```igor
TabControl MyTabControl,proc=TabActionProc,tabLabel(1)="Second Tab"
```

5. Click the second tab, which hides the first tab's controls, and then add new controls like this:

```igor
Button button1,pos={58,73},size={80,20},title="Second"
CheckBox check1,pos={60,105},size={114,15},title="Check second",value= 0
```

6. Finally, change the action procedure by adding these lines at the end:

```igor
Button button1,disable= (tc.tab!=1)
CheckBox check1,disable= (tc.tab!=1)
```

### *See Also* {#see-also}

[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls. 

[Control Panel Units](/igorpro/user-interface/controls.md#control-panel-units) for a discussion of the units used for controls.

The [ControlInfo](/igorpro/commands/controlinfo.md) operation for information about the control.

The [GetUserData](/igorpro/commands/getuserdata.md) function for retrieving named user data. 

The [ModifyControl](/igorpro/commands/modifycontrol.md) and [ModifyControlList](/igorpro/commands/modifycontrollist.md) operations.