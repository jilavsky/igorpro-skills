---
description: "The SetVariable operation creates or modifies a SetVariable control in the target window."
slug: /commands/setvariable
---

<div className="command-signature">

## <strong>SetVariable</strong>  [/Z] <em>ctrlName</em> [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#setvariable}

</div>

The SetVariable operation creates or modifies a SetVariable control in the target window.

A SetVariable control sets the value of a global numeric or string variable or a point in a wave when you type or click in the control. A SetVariable can also hold its own value without the need for a global or wave.

For information about the state or status of the control, use the [ControlInfo](/igorpro/commands/controlinfo.md) operation.

### *Parameters* {#parameters}
*ctrlName* is the name of the SetVariable control to be created or changed.

The following keyword=value parameters are supported:


|  |  |
| --- | --- |
| activate | Activates the control and selects the text that sets the value. Use [ControlUpdate](/igorpro/commands/controlupdate.md) to deactivate the control and deselect the text. |
| <span class="table-cell-nowrap">align = *alignment*</span> | Sets the alignment mode of the control. The alignment mode controls the interpretation of the *leftOrRight* parameter to the pos keyword. The align keyword was added in Igor Pro 8.00. |
|  | If *alignment*=0 (default), *leftOrRight* specifies the position of the left end of the control and the left end position remains fixed if the control size is changed. |
|  | If *alignment*=1, *leftOrRight* specifies the position of the right end of the control and the right end position remains fixed if the control size is changed. |
| <span class="table-cell-nowrap">appearance = {*kind* [, *platform* ]}</span> |  |
|  | Sets the appearance of the control. *platform* is optional. Both parameters are names, not strings. |
|  | *kind* can be one of `default`, `native`, or `os9`. |
|  | *platform* can be one of `Mac`, `Win`, or `All`. |
|  | See [Button](/igorpro/commands/button.md) and [DefaultGUIControls](/igorpro/commands/defaultguicontrols.md) for more appearance details. |
| <span class="table-cell-nowrap">bodyWidth = *width*</span> | Specifies an explicit size for the body (nontitle) portion of a SetVariable control. By default (bodyWidth=0), the body portion is the amount left over from the specified control width after providing space for the current text of the title portion. If the font, font size or text of the title changes, then the body portion may grow or shrink. If you supply a bodyWidth>0, then the body is fixed at the size you specify regardless of the body text. This makes it easier to keep a set of controls right aligned when the default font is changed. |
| <span class="table-cell-nowrap">disable = *d*</span> | Sets user editability of the control. |
|  |<table class="nested-table"><tbody><tr><td>*d*&nbsp;=0:</td><td>Normal.</td></tr><tr><td>*d*&nbsp;=1:</td><td>Hide.</td></tr><tr><td>*d*&nbsp;=2:</td><td>No user input.</td></tr></tbody></table>
| <span class="table-cell-nowrap">fColor = (*r*,*g*,*b*[,*a*])</span> | Sets the initial color of the title. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
|  | To further change the color of the title text, use escape sequences as described for title=*titleStr*. |
| <span class="table-cell-nowrap">focusRing = *fr*</span> | Enables or disables the drawing of a rectangle indicating keyboard focus: |
|  |<table class="nested-table"><tbody><tr><td>*fr*=0:</td><td>Focus rectangle will not be drawn.</td></tr><tr><td>*fr*=1:</td><td>Focus rectangle will be drawn (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">font = "*fontName*"</span> | Sets the font used to display the value of the variable, |
|  | e.g., font="Helvetica". |
| <span class="table-cell-nowrap">format = *formatStr*</span> | Sets the numeric format of the displayed value, e.g., format="%g". Not used with string variables. Never use leading text or the "%W" format for numbers, because Igor reads the value back without interpreting the extra text. For a description of *formatStr*, see the printf operation. |
| frame=*f* |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>Value is unframed.</td></tr><tr><td>*f*&nbsp;=1:</td><td>Value is framed, the default.</td></tr></tbody></table>
| <span class="table-cell-nowrap">fsize = *s*</span> | Sets the size of the type used to display the value of the variable. |
| <span class="table-cell-nowrap">fstyle = *fs*</span> | *fs* is a bitwise parameter with each bit controlling one aspect of the font style as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">guides = {*left, hcenter, right, top, vcenter, bottom*}</span> |  |
|  | Controls attachments of anchor points to layout guides. See [Laying Out Controls in Guides Mode](/igorpro/user-interface/controls.md#laying-out-controls-in-guides-mode) for detailed information and examples. |
|  | Each of *left, hcenter, right, top, vcenter, bottom* is replaced with the name of a layout guide of appropriate orientation. That is, *left, hcenter, right* indicate attachments to vertical guides, and *top, vcenter, bottom* indicate attachments to horizontal guides. Use the special name *kwNone* to represent an unattached anchor point. |
|  | An error results if you overconstrain a control's layout. A SetVariable control's height is determined by font and font sizes used for the title and value, so only one of *top, vcenter, bottom* can be attached to a layout guide. |
|  | If you use the bodyWidth keyword, the width of the control is set by the body width plus the width of the title, so you can use only one of *left, hcenter, right*. |
|  | If you do not use bodyWidth, then the value portion of the control is whatever is left over after the title width is subtracted from the overall control width, so if you use two guide attachments, they could reduce the width of the value portion to zero. |
|  | Using *kwNone* for all anchor points results in completely detaching a control from the layout guides. |
| <span class="table-cell-nowrap">help = {*helpStr* }</span> | Sets the help for the control. |
|  | *helpStr* is limited to 1970 bytes (255 in Igor Pro 8 and before). |
|  | You can insert a line break by putting "\r" in a quoted string. |
| <span class="table-cell-nowrap">labelBack = (*r*,*g*,*b*[,*a*]) or 0</span> |  |
|  | Specifies the background fill color for labels. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is 0, which uses the window's background color. |
| <span class="table-cell-nowrap">limits = {*low*,*high*,*inc* }</span> | *low* and *high* set the limits of the allowable values for the variable. *inc* sets the amount by which the variable is incremented if you click the control's up/down arrows. This applies to numeric variables, not to string variables. If *inc* is zero then the up/down arrows will not be drawn. |
| live=*l* |<table class="nested-table"><tbody><tr><td>*l*&nbsp;=0:</td><td>Update only after variable changes. Default value.</td></tr><tr><td>*l*&nbsp;=1:</td><td>Update as variable changes.</td></tr></tbody></table>
| noedit=*val* |<table class="nested-table"><tbody><tr><td>noedit=0</td><td>Reactivates user editing.</td></tr><tr><td>noedit=1</td><td>Prevents the user from clicking on (or tabbing into) a SetVariable control in order to directly edit its value. This is useful when you want to make a string read-only or when you want to restrict a numeric setting to those available only via the control&#39;s up or down arrow buttons.</td></tr><tr><td>noedit=2</td><td>Deprecated as of Igor Pro 6.34 but still supported. It allows the use of formatting escape codes described under [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes). Use styledText=1, instead.</td></tr></tbody></table>
| noproc | Specifies that no procedure is to execute when the control's value is changed. |
| <span class="table-cell-nowrap">pos = {*leftOrRight*,*top* }</span> | Sets the position in [control panel units](/igorpro/user-interface/controls.md#control-panel-units) of the top/left corner of the control if its alignment mode is 0 or the top/right corner of the control if its alignment mode is 1. See the align keyword above for details. |
| <span class="table-cell-nowrap">pos+ = {*dx,dy* }</span> | Offsets the position of the control in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">proc = *procName*</span> | Specifies the procedure to execute when the control's value is changed. |
| <span class="table-cell-nowrap">rename = *newName*</span> | Gives control a new name. |
| <span class="table-cell-nowrap">size = {*width*,*height* }</span> | Sets width of control in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). *height* is ignored. |
| <span class="table-cell-nowrap">styledText = *val*</span> | styledText=1 allows the use of use of formatting escape codes described under [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes). This works for string SetVariable controls only, not for numeric controls. |
|  | For example: |
|  | <code class="igor">SetVariable sv0 value=_STR:"\\JC\\K(65535,0,0)Centered Red Text"</code> |
|  | styledText=0 treats escape codes as plain text. |
|  | The styledText keyword was added in Igor Pro 6.34. For compatibility with earlier versions of Igor, the combination of noedit=1 and styledText=1 is recorded as noedit=2 in recreation macros. |
| <span class="table-cell-nowrap">textAlign = *t*</span> | Sets the alignment of the text displayed in the body of the control. |
|  |<table class="nested-table"><tbody><tr><td>*t*&nbsp;=0:</td><td>Left (default)</td></tr><tr><td>*t*&nbsp;=1:</td><td>Centered</td></tr><tr><td>*t*&nbsp;=2:</td><td>Right</td></tr></tbody></table>
|  | The textAlign keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">title = *titleStr*</span> | Sets the title of the control to the specified string expression. The title is displayed to the left of the control. If *titleStr* is empty (""), the name of the variable being controlled is displayed as a title. Use title="  " to create a "blank" title. |
|  | Using escape codes you can change the font, size, style and color of the title. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details. |
| <span class="table-cell-nowrap">userdata(*UDName* ) = *UDStr*</span> |  |
|  | Sets the unnamed user data to *UDStr*. Use the optional (*UDName* ) to specify a named user data to create. |
| <span class="table-cell-nowrap">userdata(*UDName* )+ = *UDStr*</span> |  |
|  | Appends *UDStr* to the current unnamed user data. Use the optional (*UDName* ) to append to the named user data. |
| <span class="table-cell-nowrap">value = *varOrWaveName*</span> | Sets the numeric or string variable or wave element to be controlled. |
|  | If *varOrWaveName* references a wave, the point is specified using standard bracket notation with either a numeric point number or a row label, e.g., value=awave[4] or value=awave[%alabel]. You may also use a  2D, 3D, or 4D wave and specify a column, layer, and chunk index or dimension label in addition to the row index. |
|  | You can have the control store the value internally rather than in a global variable. In place of *varName*, use _STR:*str* or _NUM:*num*. For example: |
|  | <code class="igor">NewPanel;SetVariable sv1,value=_NUM:123</code> |
| <span class="table-cell-nowrap">valueColor = (*r*,*g*,*b*[,*a*])</span> | Sets the color of the value text. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
| <span class="table-cell-nowrap">valueBackColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the background color under the value text. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">valueBackColor = 0</span> | Sets the background color under the value text to the default color, the standard document background color used on the current operating system, which is usually white. |
| <span class="table-cell-nowrap">win = *winName*</span> | Specifies which window or subwindow contains the named control. If not given, then the top-most graph or panel window or subwindow is assumed. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}

The target window must be a graph or panel.

### *SetVariable Action Procedure* {#setvariable-action-procedure}
The action procedure for a SetVariable control takes a predefined WMSetVariableAction structure as a parameter to the function:


```igor
Function ActionProcName(SV_Struct) : SetVariableControl
	STRUCT WMSetVariableAction &SV_Struct
	...
	return 0
End
```

The ": SetVariableControl" designation tells Igor to include this procedure in the Procedure pop-up menu in the SetVariable Control dialog.

See [WMSetVariableAction](/igorpro/programming/structures/wmsetvariableaction.md) for details on the WMSetVariableAction structure.

Although the return value is not currently used, action procedures should always return zero.

You may see an old format SetVariable action procedure in old code:


```igor
Function procName (ctrlName,varNum,varStr,varName) : SetVariableControl
	String ctrlName
	Variable varNum     // value of variable as number
	String varStr       // value of variable as string
	String varName      // name of variable
	...
	return 0
End
```

This old format should not be used in new code.

### *Examples* {#examples}
Executing the commands:


```igor
Variable/G globalVar=99
SetVariable setvar0 size={120,20}
SetVariable setvar0 font="Helvetica", value=globalVar
```

creates a SetVariable control that displays the value of globalVar.

### *See Also* {#see-also}
[printf](/igorpro/commands/printf.md) for an explanation of *formatStr*.

[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.

[Control Panel Units](/igorpro/user-interface/controls.md#control-panel-units) for a discussion of the units used for controls.

The [ControlInfo](/igorpro/commands/controlinfo.md) operation for information about the control.

The [GetUserData](/igorpro/commands/getuserdata.md) function for retrieving named user data.