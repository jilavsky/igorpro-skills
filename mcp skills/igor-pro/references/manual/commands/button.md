---
description: "The Button operation creates or modifies the named button control in the target window."
slug: /commands/button
---

<div className="command-signature">

## <strong>Button</strong>  [/Z] <em>ctrlName</em>  [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#button}

</div>

The Button operation creates or modifies the named button control in the target window.

For information about the state or status of the control, use the [ControlInfo](/igorpro/commands/controlinfo.md) operation.

### *Parameters* {#parameters}
*ctrlName*  is the name of the Button control to be created or changed.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">align = *alignment*</span> | Sets the alignment mode of the control. The alignment mode controls the interpretation of the *leftOrRight* parameter to the pos keyword. The align keyword was added in Igor Pro 8.00. |
|  | If *alignment*=0 (default), *leftOrRight* specifies the position of the left end of the control and the left end position remains fixed if the control size is changed. |
|  | If *alignment*=1, *leftOrRight* specifies the position of the right end of the control and the right end position remains fixed if the control size is changed. |
| <span class="table-cell-nowrap">appearance = {*kind*  [, *platform* ]}</span> |  |
|  | Sets the appearance of the control. *platform* is optional. Both parameters are names, not strings. |
|  |<table class="nested-table"><tbody><tr><td>*kind*&nbsp;=default:</td><td>The appearance is determined by the [DefaultGUIControls](/igorpro/commands/defaultguicontrols.md) command.</td></tr><tr><td>*kind*&nbsp;=native:</td><td>Creates standard-looking controls for the current computer platform.</td></tr><tr><td>*kind*&nbsp;=os9:</td><td>Igor Pro 5 appearance (quasi-Macintosh OS 9 controls).</td></tr><tr><td>*platform*&nbsp;=Mac:</td><td>Changes the appearance of controls on Macintosh computers running Igor 9 or earlier.</td></tr><tr><td>*platform*&nbsp;=Win:</td><td>Changes the appearance of controls on Windows computers.</td></tr><tr><td>*platform*&nbsp;=All:</td><td>Changes the appearance of controls on Windows computers and on Macintosh computers running Igor 9 or earlier.</td></tr></tbody></table>
| <span class="table-cell-nowrap">disable = *d*</span> | Sets the state of the control. *d* is a bit field: bit 0 (the least significant bit) is set when the control is hidden. Bit 1 is set when the control is disabled: |
|  |<table class="nested-table"><tbody><tr><td>*d*&nbsp;=0:</td><td>Normal (visible), enabled.</td></tr><tr><td>*d*&nbsp;=1:</td><td>Hidden.</td></tr><tr><td>*d*&nbsp;=2:</td><td>Visible and disabled. Drawn in grayed state, also disables action procedure.</td></tr><tr><td>*d*&nbsp;=3:</td><td>Hidden and disabled.</td></tr></tbody></table>
|  | See the [ModifyControl](/igorpro/commands/modifycontrol.md) example for setting the bits individually. |
| <span class="table-cell-nowrap">fColor = (*r*,*g*,*b*[,*a*])</span> | Sets color of the button. *r*, *g,* *b,* and *a* specify the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). While accepted as an input, *a* has no effect. |
|  | Specify fColor=(0,0,0) to get the default button color. If you want a black button use fColor=(1,1,1). To get the default blue button appearance, use fColor(0,0,65535). |
| To set the color of the title text, see valueColor. |  |
| <span class="table-cell-nowrap">focusRing = *fr*</span> | Enables or disables the drawing of a rectangle indicating keyboard focus: |
|  |<table class="nested-table"><tbody><tr><td>*fr*=0:</td><td>Focus rectangle will not be drawn.</td></tr><tr><td>*fr*=1:</td><td>Focus rectangle will be drawn (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">font = "*fontName* "</span> | Sets font, e.g., font="Helvetica". |
| <span class="table-cell-nowrap">fsize = *s*</span> | Sets font size. |
| <span class="table-cell-nowrap">fstyle = *fs*</span> | Specifies the font style. *fs*  is a bitwise parameter with each bit controlling one aspect of the font style as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">guides = {*left, hcenter, right, top, vcenter, bottom*}</span> |  |
|  | Controls attachments of anchor points to layout guides. See [Laying Out Controls in Guides Mode](/igorpro/user-interface/controls.md#laying-out-controls-in-guides-mode) for detailed information and examples. |
|  | Each of *left, hcenter, right, top, vcenter, bottom* is replaced with the name of a layout guide of appropriate orientation. That is, *left, hcenter, right* indicate attachments to vertical guides, and *top, vcenter, bottom* indicate attachments to horizontal guides. Use the special name *kwNone* to represent an unattached anchor point. |
|  | An error results if you overconstrain a control's layout. Of the three horizontal or vertical anchor points, at most two may be attached to layout guides. Attaching one of the three causes a control to move as the layout guide moves. Attaching two causes a control to both move and resize.  Thus, the name *kwNone* will appear at least twice. |
|  | Using *kwNone* for all anchor points results in completely detaching a control from the layout guides. |
|  | Note that if you set a picture for the button's appearance, attachments to layout guides that cause the button to change size will distort the picture. |
| <span class="table-cell-nowrap">help = {*helpStr* }</span> | Sets the help for the control. |
|  | *helpStr* is limited to 1970 bytes (255 in Igor Pro 8 and before). |
|  | You can insert a line break by putting "\r" in a quoted string. |
| <span class="table-cell-nowrap">labelBack = (*r*,*g*,*b[,a]* ) or 0</span> |  |
|  | Sets the background color for the control when using a picture to define the appearance of the button (see the picture keyword). |
|  | The labelBack keyword was added in Igor Pro 9.00. |
|  | *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
|  | For transparency to work, the picture must be inherently transparent. For example, each pixel in a PNG picture has its own internal alpha value so it can be inherently transparent or inherently opaque. |
|  | If you want the button background to be actually transparent, use the labelBack color to set the background color of the picture. In most cases, use transparent white: labelBack=(65535, 65535, 65535, 0). |
|  | If you omit labelBack or specify labelBack=0 then the button background color is the background color of the window in which the button is drawn. |
| noproc | Specifies that no procedure is to execute when clicking the button. |
| <span class="table-cell-nowrap">picture = *pict*</span> | Draws the button using the named picture. The picture is taken to be three side-by-side frames that show the control appearance in the normal state, when the mouse is down, and in the disabled state. The picture may be either a global (imported) picture or a Proc Picture (see [Proc Pictures](/igorpro/programming/programming.md#proc-pictures)). |
|  | By default, the button's rectangle is filled with the background color of the window it is drawn in before the picture is drawn. You can use the labelBack keyword to control the button's background color and transparency. |
|  | In Igor 6, the size keyword is ignored when a picture is used with a button control. To make it easier to size graphics for high-resolution screens, as of Igor 7, the size keyword is respected in this case. |
| <span class="table-cell-nowrap">pos = {*leftOrRight*,*top* }</span> | Sets the position in [control panel units](/igorpro/user-interface/controls.md#control-panel-units) of the top/left corner of the control if its alignment mode is 0 or the top/right corner of the control if its alignment mode is 1. See the align keyword above for details. |
| <span class="table-cell-nowrap">pos+ = {*dx,dy* }</span> | Offsets the position of the button in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">proc = *procName*</span> | Specifies the name of the procedure to execute when clicking the button. |
| <span class="table-cell-nowrap">rename = *newName*</span> | Gives button a new name. |
| <span class="table-cell-nowrap">size = {*width*,*height* }</span> | Sets *width* and *height* of button in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">title = *titleStr*</span> | Sets title of button to the specified string expression. The title is the text that appears in the button. If not given then title will be "New". If you use "" the button will contain no text. |
|  | Using escape codes you can change the font, size, style and color of the title. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details. |
| <span class="table-cell-nowrap">userdata(*UDName* ) = *UDStr*</span> |  |
|  | Sets the unnamed user data to *UDStr*. Use the optional (*UDName* ) to specify a named user data to create. |
| <span class="table-cell-nowrap">userdata(*UDName* )+ = *UDStr*</span> |  |
|  | Appends *UDStr*  to the current unnamed user data. Use the optional (*UDName* ) to append to the named user data. |
| <span class="table-cell-nowrap">valueColor = (*r*,*g*,*b*[,*a*])</span> | Sets initial color of the button's text (title). *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
|  | To further change the color of the title text, use escape sequences as described for title=*titleStr*. |
| <span class="table-cell-nowrap">win = *winName*</span> | Specifies which window or subwindow contains the named control. If not given, then the top-most graph or panel window or subwindow is assumed. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The target window must be a graph or panel.

### *Button Action Procedure* {#button-action-procedure}
The action procedure for a Button control takes a predefined structure WMButtonAction as a parameter to the function:


```igor
Function ActionProcName(B_Struct) : ButtonControl
	STRUCT WMButtonAction &B_Struct
	...
	return 0
End
```

The ": ButtonControl" designation tells Igor to include this procedure in the Procedure pop-up menu in the Button Control dialog.

See [WMButtonAction](/igorpro/programming/structures/wmbuttonaction.md) for details on the WMButtonAction structure.

Although the return value is not currently used, action procedures should always return zero.

You may see an old format button action procedure in old code:


```igor
Function procName (ctrlName) : ButtonControl
	String ctrlName
	...
	return 0
End
```

This old format should not be used in new code.

### *See Also* {#see-also}
[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.

[Control Panel Units](/igorpro/user-interface/controls.md#control-panel-units) for a discussion of the units used for controls.

The [ControlInfo](/igorpro/commands/controlinfo.md) operation for information about the control.

The [GetUserData](/igorpro/commands/getuserdata.md) function for retrieving named user data.

### *Demos* {#demos}
[Open All Controls Demo](#igor-pxp/Examples/Feature__Demos__2/All__Controls__Demo.pxp)