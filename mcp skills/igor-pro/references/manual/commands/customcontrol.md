---
description: "The CustomControl operation creates or modifies a custom control in the target window."
slug: /commands/customcontrol
---

<div className="command-signature">

## <strong>CustomControl</strong>  [/Z] <em>ctrlName</em>  [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#customcontrol}

</div>

The CustomControl operation creates or modifies a custom control in the target window. A CustomControl starts out as a generic button, but you can customize both its appearance and its action.

### *Parameters* {#parameters}
*ctrlName*  is the name of the Custom Control to be created or changed. See [Button](/igorpro/commands/button.md) for standard default parameters.

The following keyword=value parameters are supported:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">align = *alignment*</span> | Sets the alignment mode of the control. The alignment mode controls the interpretation of the *leftOrRight* parameter to the pos keyword. The align keyword was added in Igor Pro 8.00. |
|  | If *alignment*=0 (default), *leftOrRight* specifies the position of the left end of the control and the left end position remains fixed if the control size is changed. |
|  | If *alignment*=1, *leftOrRight* specifies the position of the right end of the control and the right end position remains fixed if the control size is changed. |
| <span class="table-cell-nowrap">fColor = (*r*,*g*,*b*[,*a*])</span> | Sets color of the button only when picture is not used and frame=1. |
|  | *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">focusRing = *fr*</span> | Enables or disables the drawing of a rectangle indicating keyboard focus: |
|  |<table class="nested-table"><tbody><tr><td>*fr*=0:</td><td>Focus rectangle will not be drawn.</td></tr><tr><td>*fr*=1:</td><td>Focus rectangle will be drawn (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">frame = *f*</span> | Sets frame style used only when picture is not used: |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>No frame (only the title is drawn).</td></tr><tr><td>*f*&nbsp;=1:</td><td>Default, a button is drawn with a centered title.</td></tr></tbody></table>
|  | Set fColor to something other than black to colorize the button. |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=2:</td><td>Simple box.</td></tr><tr><td>*f*&nbsp;=3:</td><td>3D sunken frame.</td></tr><tr><td>*f*&nbsp;=4:</td><td>3D raised frame.</td></tr><tr><td>*f*&nbsp;=5:</td><td>Text well.</td></tr></tbody></table>
| <span class="table-cell-nowrap">guides = {*left, hcenter, right, top, vcenter, bottom*}</span> |  |
|  | Controls attachments of anchor points to layout guides. See [Laying Out Controls in Guides Mode](/igorpro/user-interface/controls.md#laying-out-controls-in-guides-mode) for detailed information and examples. |
|  | Each of *left, hcenter, right, top, vcenter, bottom* is replaced with the name of a layout guide of appropriate orientation. That is, *left, hcenter, right* indicate attachments to vertical guides, and *top, vcenter, bottom* indicate attachments to horizontal guides. Use the special name *kwNone* to represent an unattached anchor point. |
|  | An error results if you overconstrain a control's layout. Of the three horizontal or vertical anchor points, at most two may be attached to layout guides. Attaching one of the three causes a control to move as the layout guide moves. Attaching two causes a control to both move and resize.  Thus, the name *kwNone* will appear at least twice. |
|  | Using *kwNone* for all anchor points results in completely detaching a control from the layout guides. |
|  | Note that a custom control's user-defined action procedure can attempt to resize the control or take other actions that could be in conflict with layout guide attachments. If the control uses a picture for the control, the picture may be distorted if the layout guides change the control's size. |
| <span class="table-cell-nowrap">help = {*helpStr* }</span> | Sets the help for the control. |
|  | *helpStr* is limited to 1970 bytes (255 in Igor Pro 8 and before). |
|  | You can insert a line break by putting "\r" in a quoted string. |
| <span class="table-cell-nowrap">labelBack = (*r*,*g*,*b*[,*a*]) or 0</span> |  |
|  | Sets background color for the control only when a picture is not used and frame is not 1. |
|  | *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). If not set (or labelBack=0), then background is transparent (not erased). |
| <span class="table-cell-nowrap">mode = *m*</span> | Notifies the control that something has happened. Can be used for any purpose. See Details discussion of the kCCE_mode event. |
| noproc | Specifies that no procedure is to execute when clicking the custom control. |
| <span class="table-cell-nowrap">picture = *pict*</span> | Uses the named Proc Picture to draw the control. Using this form of the *picture* keyword, the picture is taken to be three side-by-side frames, which show the control appearance in the normal state, when the mouse is down, and in the disabled state. |
|  | The control action function can change the number of frames using the picture={*pict*,*n* } syntax. |
|  | If the *size* keyword is not used when the control is created, the picture size sets the initial size of the control; the width is the picture width/3. Resizing the control will distort the picture. |
| <span class="table-cell-nowrap">picture = {*pict*,*n* }</span> | Uses the specified Proc Picture to draw the control. The picture is *n*  side-by-side frames instead of the default three frames. |
|  | If the *size* keyword is not used when the control is created, the picture size sets the initial size of the control; the width is the picture width/n. Resizing the control will distort the picture. |
| <span class="table-cell-nowrap">pos = {*leftOrRight*,*top* }</span> | Sets the position in [control panel units](/igorpro/user-interface/controls.md#control-panel-units) of the top/left corner of the control if its alignment mode is 0 or the top/right corner of the control if its alignment mode is 1. See the align keyword above for details. |
| <span class="table-cell-nowrap">pos+ = {*dx,dy* }</span> | Offsets the position of the control in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">proc = *procName*</span> | Specifies the name of the action function for the control. The function must not kill the control or the window. |
| <span class="table-cell-nowrap">rename = *newName*</span> | Gives the control a new name. |
| <span class="table-cell-nowrap">size = {*width*,*height* }</span> | Sets size of the control in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). If a picture is used, this may distort the picture. See the `picture` keyword. |
| <span class="table-cell-nowrap">title = *titleStr*</span> | Specifies text that appears in the control. |
|  | Using escape codes you can change the font, size, style and color of the title. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details. |
| <span class="table-cell-nowrap">userdata(*UDName* ) = *UDStr*</span> |  |
|  | Sets the unnamed user data to *UDStr*. Use the optional (*UDName* ) to specify a named user data to create. |
| <span class="table-cell-nowrap">userdata(*UDName* )+ = *UDStr*</span> |  |
|  | Appends *UDStr*  to the current unnamed user data. Use the optional (*UDName* ) to append to the named user data. |
| <span class="table-cell-nowrap">value = *varName*</span> | Sets the numeric variable, string variable, or wave that is associated with the control. With a wave, specify a point using the standard bracket notation with either a point number (`value=awave[4]`) or a row label (`value=awave[%alabel]`). |
| <span class="table-cell-nowrap">valueColor = (*r*,*g*,*b*[,*a*])</span> | Sets initial color of the title for the button drawn only when picture is not used and frame=1. |
|  | *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
|  | To further change the color of the title text, use escape sequences as described for title=*titleStr*. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
When you create a custom control, your action procedure gets information about the state of the control using the WMCustomControlAction structure. See [WMCustomControlAction](/igorpro/programming/structures/wmcustomcontrolaction.md) for details on the WMCustomControlAction structure.

Although the return value is not currently used, action procedures should always return zero.

When Igor calls your action procedure for the `kCCE_draw` event, the basic button picture (custom or default) will already have been drawn. You can use standard drawing commands such as DrawLine to draw on top of the basic picture. Unlike the normal situation when drawing commands merely add to a drawing operation list which only later is drawn, `kCCE_draw` event drawing commands are executed directly. The coordinate system, which you cannot change, is [control panel units](/igorpro/user-interface/controls.md#control-panel-units) with (0,0) being the top left corner of the control. Most drawing commands are legal but because of the immediate nature of drawing, the /A (append) flag of [DrawPoly](/igorpro/commands/drawpoly.md) is not allowed.

The `kCCE_mode` event, which Igor sends when you execute CustomControl with the mode keyword, can be used for any purpose, but it mainly serves as a notification to the control that something has happened. For example, to send information to a control, you can set a named (or the unnamed) userdata and then set the mode to indicate that the control should examine the userdata. For this signaling purpose, you should use a mode value of 0 because this value will not become part of the recreation macro.

The `kCCE_frame` event is sent just before drawing one of the *pict* frames, as set by the picture parameter. On input, the curFrame field is set to 0 (normal or mouse down outside button), to 1 (mouse down in button), or to 2 (disable). You may modify curFrame as desired but your value will be clipped to a valid value.

When you specify a *pict*  with the picture parameter, you will get a `kCCE_drawOSBM` event when that *pict*  is drawn into an offscreen bitmap. Once it is created, all updates use the offscreen bitmap until you specify a new picture parameter. Thus the custom drawing done at this event is static, unlike drawing done during the `kCCE_draw` event, which can be different each time the control is drawn. Because the *pict* can be contain multiple side-by-side frames, the width of the offscreen bitmap is the width derived from the ctrlRect field multiplied by the number of frames.

Because the action function is called in the middle of various control events, it must not kill the control or the window. Doing so will almost certainly cause a crash.

### *CustomControl Action Procedure* {#customcontrol-action-procedure}
The action procedure for a CustomControl control takes a predefined structure WMCustomControlAction as a parameter to the function:


```igor
Function ActionProcName(s)
	STRUCT WMCustomControlAction& s
	...
	return 0
End
```

See [WMCustomControlAction](/igorpro/programming/structures/wmcustomcontrolaction.md) for details on the WMCustomControlAction structure.

Although the return value is not currently used, action procedures should always return zero.

The action procedure may have drawing commands such as [SetDrawEnv](/igorpro/commands/setdrawenv.md), [DrawRect](/igorpro/commands/drawrect.md), etc. These commands include a /W flag that directs their action to a particular window or subwindow. However, in a CustomControl action procedure, the /W flag is ignored and all drawing commands are directed to the window or subwindow containing the control.

Because the action procedure runs during a drawing operation that cannot be interrupted without crashing Igor, the debugger cannot be invoked while it is running. Consequently breakpoints set in the function are ignored. Use [Debugging with Print Statements](/igorpro/programming/debugging.md#debugging-with-print-statements) instead.

### *Examples* {#examples}
See [Creating Custom Controls](/igorpro/user-interface/controls.md#creating-custom-controls) for some examples of custom controls.

For a demonstration of custom controls, see the Custom Control Demo.pxp example experiment, which is located in your Igor Pro Folder in the `Examples:Feature Demos 2:` folder.

### *See Also* {#see-also}
[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.

[Control Panel Units](/igorpro/user-interface/controls.md#control-panel-units) for a discussion of the units used for controls.

The [ControlInfo](/igorpro/commands/controlinfo.md) operation for information about the control.

The [GetUserData](/igorpro/commands/getuserdata.md) function for retrieving named user data.

[Proc Pictures](/igorpro/programming/programming.md#proc-pictures)

[TextBox](/igorpro/commands/textbox.md), [DrawPoly](/igorpro/commands/drawpoly.md), [DefaultGUIControls](/igorpro/commands/defaultguicontrols.md)

### *Demos* {#demos}
[Open Custom Control Demo](#igor-pxp/Examples/Feature__Demos__2/Custom__Control__Demo.pxp)