---
description: "The CheckBox operation creates or modifies a checkbox, radio button or disclosure triangle in the target or named window which must be a graph or control panel."
slug: /commands/checkbox
---

<div className="command-signature">

## <strong>CheckBox</strong>  [/Z] <em>ctrlName</em>  [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#checkbox}

</div>

The CheckBox operation creates or modifies a checkbox, radio button or disclosure triangle in the target or named window which must be a graph or control panel.

*ctrlName* is the name of the checkbox.

For information about the state or status of the control, use the [ControlInfo](/igorpro/commands/controlinfo.md) operation.

### *Parameters* {#parameters}
The following keyword=value parameters are supported:

*ctrlName* is the name of the CheckBox control to be created or changed.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">align = *alignment*</span> | Sets the alignment mode of the control. The alignment mode controls the interpretation of the *leftOrRight* parameter to the pos keyword. The align keyword was added in Igor Pro 8.00. |
|  | If *alignment*=0 (default), *leftOrRight* specifies the position of the left end of the control and the left end position remains fixed if the control size is changed. |
|  | If *alignment*=1, *leftOrRight* specifies the position of the right end of the control and the right end position remains fixed if the control size is changed. |
| <span class="table-cell-nowrap">appearance = {*kind*  [, *platform* ]}</span> |  |
|  | Sets the appearance of the control. *platform*  is optional. Both parameters are names, not strings. |
|  | *kind*  can be one of default, native, or os9. |
|  | *platform*  can be one of Mac, Win, or All. |
|  | See [Button](/igorpro/commands/button.md) and [DefaultGUIControls](/igorpro/commands/defaultguicontrols.md) for more appearance details. |
| <span class="table-cell-nowrap">disable = *d*</span> | Sets user editability of the control. |
|  |<table class="nested-table"><tbody><tr><td>*d*=0:</td><td>Normal.</td></tr><tr><td>*d*=1:</td><td>Hide.</td></tr><tr><td>*d*=2:</td><td>Disable user input.</td></tr></tbody></table>
| <span class="table-cell-nowrap">fColor = (*r*,*g*,*b*[,*a*])</span> | Sets the initial color of the title. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
|  | To further change the color of the title text, use escape sequences as described for title=*titleStr*. |
| <span class="table-cell-nowrap">focusRing = *fr*</span> | Enables or disables the drawing of a rectangle indicating keyboard focus: |
|  |<table class="nested-table"><tbody><tr><td>*fr*=0:</td><td>Focus rectangle will not be drawn.</td></tr><tr><td>*fr*=1:</td><td>Focus rectangle will be drawn (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">fsize = *s*</span> | Sets font size for checkbox. |
| <span class="table-cell-nowrap">guides = {*left, hcenter, right, top, vcenter, bottom*}</span> |  |
|  | Controls attachments of anchor points to layout guides. See [Laying Out Controls in Guides Mode](/igorpro/user-interface/controls.md#laying-out-controls-in-guides-mode) for detailed information and examples. |
|  | Each of *left, hcenter, right, top, vcenter, bottom* is replaced with the name of a layout guide of appropriate orientation. That is, *left, hcenter, right* indicate attachments to vertical guides, and *top, vcenter, bottom* indicate attachments to horizontal guides. Use the special name *kwNone* to represent an unattached anchor point. |
|  | An error results if you overconstrain a control's layout. Both the width and height of a checkbox control are set by the font and font size and the length of the title. Consequently, only one anchor may be attached to layout guides in each direction, as attaching two anchor points would most likely result in an attempt to resize the checkbox control. |
|  | Using *kwNone* for all anchor points results in completely detaching a control from the layout guides. |
| <span class="table-cell-nowrap">help = {*helpStr* }</span> | Sets the help for the control. |
|  | *helpStr* is limited to 1970 bytes (255 in Igor Pro 8 and before). |
|  | You can insert a line break by putting "\r" in a quoted string. |
| <span class="table-cell-nowrap">labelBack = (*r*,*g*,*b[,a]* ) or 0</span> |  |
|  | Sets the background color of the CheckBox. |
|  | The labelBack keyword was added in Igor Pro 9.00. |
|  | *r*, *g,* *b,* and *a* specify the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
|  | If you omit labelBack or specify labelBack=0, then the background color is that of the window in which the CheckBox is drawn. |
| <span class="table-cell-nowrap">mode = *m*</span> | Specifies checkbox appearance. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=1:</td><td>Display as a radio button control.</td></tr><tr><td>*m*&nbsp;=0:</td><td>Default checkbox appearance.</td></tr></tbody></table>
| <span class="table-cell-nowrap">*m* = 2:</span> | Display as a treeview expansion node. |
| noproc | Specifies that no procedure is to execute when the checkbox is clicked. |
| <span class="table-cell-nowrap">picture = *pict*</span> | Draws the checkbox using the named picture. The picture is taken to be six side-by-side frames which show the control appearance in the normal state, when the mouse is down, and in the disabled state. The first three frames are used when the checked state is false and the next three show the true state. The picture may be either a global (imported) picture or a Proc Picture (see [Proc Pictures](/igorpro/programming/programming.md#proc-pictures)). |
| <span class="table-cell-nowrap">pos = {*leftOrRight*,*top* }</span> | Sets the position in [control panel units](/igorpro/user-interface/controls.md#control-panel-units) of the top/left corner of the control if its alignment mode is 0 or the top/right corner of the control if its alignment mode is 1. See the align keyword above for details. |
| <span class="table-cell-nowrap">pos+ = {*dx,dy* }</span> | Offsets the position of the checkbox in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">proc = *procName*</span> | Specifies the procedure to execute when the checkbox is clicked. |
| <span class="table-cell-nowrap">rename = *newName*</span> | Gives checkbox a new name. |
| side=*s* |<table class="nested-table"><tbody><tr><td>*s*&nbsp;=0:</td><td>Checkbox is on the left, title is on the right (default).</td></tr><tr><td>*s*&nbsp;=1:</td><td>Checkbox is on the right, title is on the left.</td></tr></tbody></table>
| <span class="table-cell-nowrap">size = {*width*,*height* }</span> | Sets *width* and *height* of control in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">title = *titleStr*</span> | Sets title of checkbox to the specified string expression. The title is the text that appears in the checkbox. If not given or if "" then title will be "New". |
|  | Using escape codes you can change the font, size, style and color of the title. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details. |
| <span class="table-cell-nowrap">userdata(*UDName* ) = *UDStr*</span> |  |
|  | Sets the unnamed user data to *UDStr*. Use the optional (*UDName* ) to specify a named user data to create. |
| <span class="table-cell-nowrap">userdata(*UDName* )+ = *UDStr*</span> |  |
|  | Appends *UDStr*  to the current unnamed user data. Use the optional (*UDName* ) to append to the named user data. |
| <span class="table-cell-nowrap">value = *v*</span> | Specifies whether the checkbox is selected (*v* =1) or not (*v* =0). |
| <span class="table-cell-nowrap">variable = *varName*</span> | Specifies a global numeric variable to be set to the current state of a checkbox whenever it is clicked or when it is set by the value keyword. The variable is two-way: setting the variable also changes the state of the checkbox. |
| <span class="table-cell-nowrap">wave = *waveName*</span> | Specifies a point from a wave to be set to the current state of a checkbox when it is clicked or when it is set by the value keyword. The point is specified using standard bracket notation with either a numeric point number or a row label, e.g., value=awave[4] or value=awave[%alabel]. You may also use a 2D, 3D, or 4D wave and specify a column, layer, and chunk index or dimension label in addition to the row index. This feature was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">win = *winName*</span> | Specifies which window or subwindow contains the named control. If not given, then the top-most graph or panel window or subwindow is assumed. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The target window must be a graph or panel.

### *Checkbox Action Procedure* {#checkbox-action-procedure}
The action procedure for a CheckBox control takes a predefined structure WMCheckboxAction as a parameter to the function:


```igor
Function ActionProcName(CB_Struct) : CheckBoxControl
	STRUCT WMCheckboxAction &CB_Struct
	...
	return 0
End
```

The ": CheckBoxControl" designation tells Igor to include this procedure in the Procedure pop-up menu in the CheckBox Control dialog.

See [WMCheckboxAction](/igorpro/programming/structures/wmcheckboxaction.md) for details on the WMCheckboxAction structure.

Although the return value is not currently used, action procedures should always return zero.

You may see an old format checkbox action procedure in old code:


```igor
Function procName (ctrlName,checked) : CheckBoxControl
	String ctrlName
	Variable checked	// 1 if selected, 0 if not
	...
	return 0
End
```

This old format should not be used in new code.

When using radio button controls, it is the responsibility of the Igor programmer to turn off other radio buttons when one of a group of radio buttons is pressed.

### *Examples* {#examples}

```igor
// Create a radio button group

Window Panel0() : Panel
	PauseUpdate; Silent 1		// building window...
	NewPanel /W=(150,50,353,212)
	Variable/G gSelectedRadioButton = 1
	CheckBox radioButton1,pos={52,25},size={78,15},title="Radio 1",value= 1,mode=1,proc=MyRadioButtonProc
	CheckBox radioButton2,pos={52,45},size={78,15},title="Radio 2",value= 0,mode=1,proc=MyRadioButtonProc
	CheckBox radioButton3,pos={52,65},size={78,15},title="Radio 3",value= 0,mode=1,proc=MyRadioButtonProc
EndMacro

static Function HandleRadioButtonClick(controlName)
	String controlName
	
	NVAR gSelectedRadioButton = root:gSelectedRadioButton

	strswitch(controlName)
		case "radioButton1":
			gSelectedRadioButton = 1
			break
		case "radioButton2":
			gSelectedRadioButton = 2
			break
		case "radioButton3":
			gSelectedRadioButton = 3
			break
	endswitch
	CheckBox radioButton1, value = gSelectedRadioButton==1
	CheckBox radioButton2, value = gSelectedRadioButton==2
	CheckBox radioButton3, value = gSelectedRadioButton==3
End

Function MyRadioButtonProc(cb) : CheckBoxControl
	STRUCT WMCheckboxAction& cb
	
	switch(cb.eventCode)
		case 2:		// Mouse up
			HandleRadioButtonClick(cb.ctrlName)
			break
	endswitch

	return 0
End
```

### *See Also* {#see-also}
[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.

[Control Panel Units](/igorpro/user-interface/controls.md#control-panel-units) for a discussion of the units used for controls.

The [ControlInfo](/igorpro/commands/controlinfo.md) operation for information about the control.

The [GetUserData](/igorpro/commands/getuserdata.md) function for retrieving named user data.