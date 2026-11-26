---
description: "The Slider operation creates or modifies a Slider control in the target window."
slug: /commands/slider
---

<div className="command-signature">

## <strong>Slider</strong>  [/Z] <em>ctrlName</em>  [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#slider}

</div>

The Slider operation creates or modifies a Slider control in the target window.

A Slider control sets or displays a single numeric value. The user can adjust the value by dragging a thumb along the length of the Slider.

For information about the state or status of the control, use the [ControlInfo](/igorpro/commands/controlinfo.md) operation.

### *Parameters* {#parameters}
*ctrlName* is the name of the Slider control to be created or changed.

The following keyword=value parameters are supported:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">align = *alignment*</span> | Sets the alignment mode of the control. The alignment mode controls the interpretation of the *leftOrRight* parameter to the pos keyword. The align keyword was added in Igor Pro 8.00. |
|  | If *alignment*=0 (default), *leftOrRight* specifies the position of the left end of the control and the left end position remains fixed if the control size is changed. |
|  | If *alignment*=1, *leftOrRight* specifies the position of the right end of the control and the right end position remains fixed if the control size is changed. |
| <span class="table-cell-nowrap">appearance = {*kind* [, *platform* ]}</span> |  |
|  | Sets the appearance of the control. *platform* is optional. Both parameters are names, not strings. |
|  | *kind* can be one of default or native. |
|  | *platform* can be Win or All. |
|  | See [Button](/igorpro/commands/button.md) and [DefaultGUIControls](/igorpro/commands/defaultguicontrols.md) for more appearance details. |
| <span class="table-cell-nowrap">disable = *d*</span> | Sets user editability of the control. |
|  |<table class="nested-table"><tbody><tr><td>*d*=0:</td><td>Normal.</td></tr><tr><td>*d*=1:</td><td>Hide.</td></tr><tr><td>*d*=2:</td><td>Draw in gray state; disable control action.</td></tr></tbody></table>
| <span class="table-cell-nowrap">fColor = (*r*,*g*,*b*[,*a*])</span> | Sets the color of the tick marks. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
| <span class="table-cell-nowrap">focusRing = *fr*</span> | Enables or disables the drawing of a rectangle indicating keyboard focus: |
|  |<table class="nested-table"><tbody><tr><td>*fr*=0:</td><td>Focus rectangle will not be drawn.</td></tr><tr><td>*fr*=1:</td><td>Focus rectangle will be drawn (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">font = "*fontName* "</span> | Sets the font used to display the tick labels, e.g., font="Helvetica". |
| <span class="table-cell-nowrap">fsize = *s*</span> | Sets the size of the type for tick mark labels. |
| <span class="table-cell-nowrap">guides = {*left, hcenter, right, top, vcenter, bottom*}</span> |  |
|  | Controls attachments of anchor points to layout guides. See [Laying Out Controls in Guides Mode](/igorpro/user-interface/controls.md#laying-out-controls-in-guides-mode) for detailed information and examples. |
|  | Each of *left, hcenter, right, top, vcenter, bottom* is replaced with the name of a layout guide of appropriate orientation. That is, *left, hcenter, right* indicate attachments to vertical guides, and *top, vcenter, bottom* indicate attachments to horizontal guides. Use the special name *kwNone* to represent an unattached anchor point. |
|  | An error results if you overconstrain a control's layout. |
|  | A vertically oriented Slider control (*vert*=1) has width set by the control, so you can only attach a single guide from *left, hcenter, right*. The height is user settable, allowing two guide attachments from *top, vcenter, bottom*. |
|  | A horizontally oriented Slider control (*vert*=0) has height set by the control, so you can only attach a single guide from *top, vcenter, bottom*. The width is user settable, allowing two guide attachments from *left, hcenter, right*. |
|  | Using *kwNone* for all anchor points results in completely detaching a control from the layout guides. |
| <span class="table-cell-nowrap">help = {*helpStr* }</span> | Sets the help for the control. |
|  | *helpStr* is limited to 1970 bytes (255 in Igor Pro 8 and before). |
|  | You can insert a line break by putting "\r" in a quoted string. |
| <span class="table-cell-nowrap">labelBack = (*r*,*g*,*b[,a]*) or 0</span> |  |
|  | Sets the background color of the Slider control. |
|  | The labelBack keyword was added in Igor Pro 9.00. |
|  | *r*, *g,* *b,* and *a* specify the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
|  | If you omit labelBack or specify labelBack=0, then the background color is that of the window in which the Slider is drawn. |
| <span class="table-cell-nowrap">limits = {*low*,*high*,*inc* }</span> | *low* sets left or bottom value, *high* sets right or top value. Use *inc* =0 for continuous or use desired increment between stops. |
| live=*l* |<table class="nested-table"><tbody><tr><td>*l*&nbsp;=0:</td><td>Update only after mouse is released.</td></tr><tr><td>*l*&nbsp;=1:</td><td>Update as slider is moved. Default value.</td></tr></tbody></table>
| noproc | Specifies that no procedure is to execute when the control's value is changed. |
| <span class="table-cell-nowrap">pos = {*leftOrRight*,*top* }</span> | Sets the position in [control panel units](/igorpro/user-interface/controls.md#control-panel-units) of the top/left corner of the control if its alignment mode is 0 or the top/right corner of the control if its alignment mode is 1. See the align keyword above for details. |
| <span class="table-cell-nowrap">pos+ = {*dx,dy* }</span> | Offsets the position of the slider in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">proc = *procName*</span> | Specifies the action procedure for the slider. |
| <span class="table-cell-nowrap">rename = *newName*</span> | Gives control a new name. |
| <span class="table-cell-nowrap">repeat = {*style,springback,rate,restingValue*}</span> |  |
|  | Set the control to call its action procedure repeatedly at timed intervals while the user clicks the thumb. This feature was added in Igor Pro 8.00. |
|  | *style* can take one of the following values: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>No repeat (default). Use this to turn the repeat feature off.</td></tr><tr><td>1:</td><td>Slider repeats at a constant rate.</td></tr><tr><td>2:</td><td>Slider repeats at a rate proportional to the distance from the *restingValue*.</td></tr></tbody></table>
|  | *springback* controls what happens to the slider value when the user releases the mouse. If *springback* is 1, the slider returns to the resting value. If it is 0, it remains at the last set value. |
|  | *rate* specifies the rate at which the action procedure is called in calls per second. The maximum rate accepted rate is 1000. If rate is 0, it sets *style* to 0 which turns the repeating feature off. |
|  | *restingValue* specifies the value to which the slider returns when the user releases the mouse. If *springback* is 1, the thumb automatically returns to *restingValue* when the mouse button is released. If *springback* is 0, *restingValue* has no effect. |
| side=*s* |<table class="nested-table"><tbody><tr><td>*s*&nbsp;=0:</td><td>Thumb is blunt and tick marks are suppressed.</td></tr><tr><td>*s*&nbsp;=1:</td><td>Thumb points right or down. Default value.</td></tr><tr><td>*s*&nbsp;=2:</td><td>Thumb points up or left.</td></tr></tbody></table>
| <span class="table-cell-nowrap">size = {*width*,*height* }</span> | Sets width or height of control in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). *height* is ignored if vert=0 and *width* is ignored if vert=1. |
| <span class="table-cell-nowrap">thumbColor = (*r*,*g*,*b*[,*a*])</span> | If *appearance={os9}* is in effect, sets dominant foreground color of thumb. Only the hue and saturation are used. Therefore (0,1000,0) is the same tint of green as (0,10000,0). Alpha (*a*) is accepted but ignored. |
| ticks=*t* |<table class="nested-table"><tbody><tr><td>*t*&nbsp;=0:</td><td>No ticks.</td></tr><tr><td>*t*&nbsp;=1:</td><td>Number of ticks calculated from limits (no ticks drawn if calculated value is &lt;2 or &gt;100). Default value.</td></tr><tr><td>*t*&nbsp;&gt;1:</td><td>*t* is number of ticks distributed between start and stop position. Ticks are labeled using the same automatic algorithm used for graph axes. Use negative tick values to force ticks to not be labeled. Ticks are shown on side specified by side keyword and are not drawn if side=0.</td></tr></tbody></table>
| <span class="table-cell-nowrap">tkLblRot = *deg*</span> | Rotates tick labels. *deg* is a value between -360 and 360. |
| <span class="table-cell-nowrap">userdata(*UDName*) = *UDStr*</span> |  |
|  | Sets the unnamed user data to *UDStr*. Use the optional (*UDName*) to specify a named user data to create. |
| <span class="table-cell-nowrap">userdata(*UDName*)+ = *UDStr*</span> |  |
|  | Appends *UDStr* to the current unnamed user data. Use the optional (*UDName*) to append to the named user data. |
| <span class="table-cell-nowrap">userTicks = {*tvWave*,*tlblWave* }</span> |  |
|  | User-defined tick positions and labels. *tvWave* contains the tick positions, and text wave *tlblWave* contains the labels. See discussion of the userticks keyword under [ModifyGraph](/igorpro/commands/modifygraph.md) for more info. Overrides normal ticking specified by ticks keyword. |
| <span class="table-cell-nowrap">value = *v*</span> | *v* is the new value for the Slider. |
| <span class="table-cell-nowrap">valueColor = (*r*,*g*,*b*[,*a*])</span> | Sets the color of the tick labels. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
| <span class="table-cell-nowrap">variable = *var*</span> | Sets the variable (*var*) that the slider will update. It is not necessary to connect a Slider to a variable - you can get a Slider's value using the [ControlInfo](/igorpro/commands/controlinfo.md) operation |
| <span class="table-cell-nowrap">vert = *v*</span> | Set vertical (*v* =1; default) or horizontal (*v* =0) orientation of the slider. |
| <span class="table-cell-nowrap">win = *winName*</span> | Specifies which window or subwindow contains the named control. If not given, then the top-most graph or panel window or subwindow is assumed. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The target window must be a graph or panel.

If you use negative ticks to suppress automatic labeling, you can label tick marks using drawing tools (panels only).

### *Slider Action Procedure* {#slider-action-procedure}
The action procedure for a Slider control takes a predefined WMSliderAction structure as a parameter to the function:


```igor
Function ActionProcName(S_Struct) : SliderControl
	STRUCT WMSliderAction &S_Struct
	...
	return 0
End
```

The ": SliderControl" designation tells Igor to include this procedure in the Procedure pop-up menu in the Slider Control dialog.

See [WMSliderAction](/igorpro/programming/structures/wmslideraction.md) for details on the WMSliderAction structure.

See [Handling Slider Events](/igorpro/user-interface/controls.md#handling-slider-events) for a demonstration of slider event handling.

Although the return value is not currently used, action procedures should always return zero.

This old format for a slider action procedure should not be used in new code:


```igor
Function MySliderProc(name, value, event) : SliderControl
	String name		// name of this slider control
	Variable value	// value of slider
	Variable event	// bit field: bit 0: value set; 1: mouse down, 
						//   2: mouse up, 3: mouse moved
						
	return 0			// other return values reserved
End
```

### *Repeating Sliders* {#repeating-sliders}
A repeating slider calls your action procedure periodically while the user is clicking the thumb. See [Repeating Sliders](/igorpro/user-interface/controls.md#repeating-sliders) for an overview.

When the repeat style is set to 2 (proportional rate) the rate is computed as

$$
\displaystyle { Rate }_{ {max }} \cdot \frac{\left(V_{ {rest }}-V_{{thumb }}\right)}{\max \left(a b s\left(V_{{left }}-V_{{rest }}\right), a b s\left(V_{{right }}-V_{{rest }}\right)\right)}
$$

V<sub>rest</sub> is the *restingValue*, V<sub>thumb</sub> is the value corresponding to the slider's thumb position, V<sub>left</sub> is the value at the left or bottom end of the slider and V<sub>right</sub> is the value at the right or top of the slider. The proportion is based on the larger distance of the resting value from either the right or left.

Whereas the rate can be set as high as 1000 calls per second, if your action procedure takes more time to execute than the period of the slider repeat, you will simply lose repeats. It is unlikely that a rate of more than about 50 calls per second can realistically be achieved.

### *Examples* {#examples}

```igor
Function SliderExample()
	NewPanel /W=(150,50,501,285)
	Variable/G var1
	Execute "ModifyPanel cbRGB=(56797,56797,56797)"
	SetVariable setvar0,pos={141,18},size={122,17},limits={-Inf,Inf,1},value= var1
	Slider foo,pos={26,31},size={62,143},limits={-5,10,1},variable= var1
	Slider foo2,pos={173,161},size={150,53}
	Slider foo2,limits={-5,10,1},variable= var1,vert= 0,thumbColor= (0,1000,0)
	Slider foo3,pos={80,31},size={62,143}
	Slider foo3,limits={-5,10,1},variable= var1,side= 2,thumbColor= (1000,1000,0)
	Slider foo4,pos={173,59},size={150,13}
	Slider foo4,limits={-5,10,1},variable= var1,side= 0,vert= 0,thumbColor= (1000,1000,1000)
	Slider foo5,pos={173,90},size={150,53}
	Slider foo5,limits={-5,10,1},variable= var1,side= 2,vert= 0,ticks= 5,thumbColor= (500,1000,1000)
End
```

### *See Also* {#see-also}
[Controls and Control Panels](/igorpro/user-interface/controls.md), [Handling Slider Events](/igorpro/user-interface/controls.md#handling-slider-events)

### *Demos* {#demos}
[Open Slider Demo](#igor-pxp/Examples/Feature__Demos__2/Slider__Labels.pxp)

[Open Slider Repeat Demo](#igor-pxp/Examples/Feature__Demos__2/Slider__Repeat__Demo.pxp)