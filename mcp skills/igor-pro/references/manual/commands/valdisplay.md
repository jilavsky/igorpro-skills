---
description: "The ValDisplay operation creates or modifies the named control that displays a numeric value in the target window. The appearance of the control varies."
slug: /commands/valdisplay
---

<div className="command-signature">

## <strong>ValDisplay</strong>  [/Z] <em>ctrlName</em>  [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#valdisplay}

</div>

The ValDisplay operation creates or modifies the named control that displays a numeric value in the target window. The appearance of the control varies.

For information about the state or status of the control, use the [ControlInfo](/igorpro/commands/controlinfo.md) operation.

### *Parameters* {#parameters}
*ctrlName* is the name of the ValDisplay control to be created or changed.

The following keyword=value parameters are supported:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">align = *alignment*</span> | Sets the alignment mode of the control. The alignment mode controls the interpretation of the *leftOrRight* parameter to the pos keyword. The align keyword was added in Igor Pro 8.00. |
|  | If *alignment*=0 (default), *leftOrRight* specifies the position of the left end of the control and the left end position remains fixed if the control size is changed. |
|  | If *alignment*=1, *leftOrRight* specifies the position of the right end of the control and the right end position remains fixed if the control size is changed. |
| <span class="table-cell-nowrap">appearance = {*kind* [, *platform*]}</span> |  |
|  | Sets the appearance of the control. *platform* is optional. Both parameters are names, not strings. |
|  | *kind* can be one of `default`, `native`, or `os9`. |
|  | *platform* can be one of `Mac`, W`in, or `All`. |
|  | See [Button](/igorpro/commands/button.md) and [DefaultGUIControls](/igorpro/commands/defaultguicontrols.md) for more appearance details. |
| <span class="table-cell-nowrap">barBackColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the background color under the bar (if any). *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">barBackColor = 0</span> | Sets the background color under the bar to the default color, the standard document background color used on the current operating system, which is usually white. |
| <span class="table-cell-nowrap">barmisc = {*lts*, *valwidth*}</span> |  |
|  | Sets the "limits text size" and the size of the type showing the bar limits. If *lts* is zero, the bar limits are not displayed. Otherwise, *lts* must be between 5 and 100. |
|  | *valwidth* is the "value readout width". It claims the amount of horizontal space for the numeric part of the display. |
|  | If *valwidth* equals or exceeds the control width available to it, the numeric readout uses all the room, and prevents display of any bar. |
|  | If *valwidth* is zero, there is no numeric readout, and only the bar is displayed. |
|  | *valwidth* can range from zero to 4000, and it defaults to 1000 (which usually leaves no room for the display bar). |
| <span class="table-cell-nowrap">bodyWidth = *width*</span> | Specifies an explicit size for the body (nontitle) portion of a ValDisplay control. By default (bodyWidth=0), the body portion is the amount left over from the specified control width after providing space for the current text of the title portion. If the font, font size, or text of the title changes, then the body portion may grow or shrink. If you supply a bodyWidth>0, then the body is fixed at the size you specify regardless of the body text. This makes it easier to keep a set of controls right aligned when the default font is changed. |
| <span class="table-cell-nowrap">disable = *d*</span> | Sets user editability of the control. |
|  |<table class="nested-table"><tbody><tr><td>*d*=0:</td><td>Normal.</td></tr><tr><td>*d*=1:</td><td>Hide.</td></tr><tr><td>*d*=2:</td><td>Disable user input. Does not change control appearance because it is read-only.</td></tr></tbody></table>
| <span class="table-cell-nowrap">fColor = (*r*,*g*,*b*[,*a*])</span> | Sets the initial color of the title. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
|  | To further change the color of the title text, use escape sequences as described for title=*titleStr*. |
| <span class="table-cell-nowrap">font = "*fontName*"</span> | Sets the font used to display the value of the variable, |
|  | e.g., font="Helvetica". |
| <span class="table-cell-nowrap">format = *formatStr*</span> | Sets the numeric format of the displayed value. The default format is "%g". For a description of *formatStr*, see the [printf](/igorpro/commands/printf.md) operation. |
| <span class="table-cell-nowrap">frame = *f*</span> | Sets frame style. |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>Value is unframed.</td></tr><tr><td>*f*&nbsp;=1:</td><td>Value is framed, the default (same as *f* =3).</td></tr><tr><td>*f*&nbsp;=2:</td><td>Simple box.</td></tr><tr><td>*f*&nbsp;=3:</td><td>3D sunken frame.</td></tr><tr><td>*f*&nbsp;=4:</td><td>3D raised frame.</td></tr><tr><td>*f*&nbsp;=5:</td><td>Text well.</td></tr></tbody></table>
| <span class="table-cell-nowrap">fsize = *s*</span> | Sets the size of the type used to display the value in the numeric readout. The default is 12 points. |
| <span class="table-cell-nowrap">fstyle = *fs*</span> | *fs* is a bitwise parameter with each bit controlling one aspect of the font style as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">guides = {*left, hcenter, right, top, vcenter, bottom*}</span> |  |
|  | Controls attachments of anchor points to layout guides. See [Laying Out Controls in Guides Mode](/igorpro/user-interface/controls.md#laying-out-controls-in-guides-mode) for detailed information and examples. |
|  | Each of *left, hcenter, right, top, vcenter, bottom* is replaced with the name of a layout guide of appropriate orientation. That is, *left, hcenter, right* indicate attachments to vertical guides, and *top, vcenter, bottom* indicate attachments to horizontal guides. Use the special name *kwNone* to represent an unattached anchor point. |
|  | An error results if you overconstrain a control's layout. A ValDisplay control's height is determined by font and font sizes used for the various parts of the control, so only one of *top, vcenter, bottom* can be attached to a layout guide. |
|  | If you use the *bodyWidth* keyword, the width of the control is set by the body width plus the width of the other parts, so you can use only one of *left, hcenter, right*. |
|  | If you do not use *bodyWidth*, then the width of the value portion of the control is whatever is left over after the width of other parts is subtracted from the overall control width, so if you use two guide attachments, they could reduce the width of the value portion to zero. |
|  | Using *kwNone* for all anchor points results in completely detaching a control from the layout guides. |
| <span class="table-cell-nowrap">help = {*helpStr*}</span> | Sets the help for the control. |
|  | *helpStr* is limited to 1970 bytes (255 in Igor Pro 8 and before). |
|  | You can insert a line break by putting "\\r" in a quoted string. |
| <span class="table-cell-nowrap">highColor = (*r*,*g*,*b*[,*a*])</span> | Specifies the bar color when the value is greater than *base* in the limits keyword. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">labelBack = (*r*,*g*,*b*[,*a*]) or 0</span> |  |
|  | Specifies the background fill color for labels. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is 0, which uses the window's background color. |
| <span class="table-cell-nowrap">limits = {*low*,*high*,*base*}</span> |  |
|  | Controls how the value is translated into a graphical representation when the display includes a bar (described fully in Details). Defaults are {0,0,0}, which aren't too useful. |
| <span class="table-cell-nowrap">limitsColor = (*r*,*g*,*b*[,*a*])</span> | Sets the color of the limits text, if any. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">limitsBackColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the background color under the limits text. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">limitsBackColor = 0</span> | Sets the background color under the limits text to the default color, the standard document background color used on the current operating system, which is usually white. |
| <span class="table-cell-nowrap">lowColor = (*r*,*g*,*b*[,*a*])</span> | Specifies the bar color when the value is less than *base* in the limits keyword. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">mode = *m*</span> | Specifies the type of LED display to use, if any. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Bar mode (default).</td></tr><tr><td>*m*&nbsp;=1:</td><td>Oval LED</td></tr><tr><td>*m*&nbsp;=2:</td><td>Rectangular LED.</td></tr><tr><td>*m*&nbsp;=3:</td><td>Bar mode with no fractional part.</td></tr><tr><td>*m*&nbsp;=4:</td><td>Candy-stripe effect for the bar area to support indefinite-style progress windows. The value is taken to be the phase of the candy stripe. When using value= _NUM:n, n is taken as an increment value so you would normally just use 1. Uses the native platform appearance if the high and low colors are left as default. Note native formats may not fill vertical space. See [Progress Windows](/igorpro/programming/interacting-with-the-user.md#progress-windows) for an example.</td></tr></tbody></table>
| <span class="table-cell-nowrap">pos = {*leftOrRight*,*top*}</span> | Sets the position in [control panel units](/igorpro/user-interface/controls.md#control-panel-units) of the top/left corner of the control if its alignment mode is 0 or the top/right corner of the control if its alignment mode is 1. See the align keyword above for details. |
| <span class="table-cell-nowrap">pos+ = {*dx,dy*}</span> | Offsets the position of the display in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">rename = *newName*</span> | Gives the ValDisplay control a new name. |
| <span class="table-cell-nowrap">size = {*width*,*height*}</span> | Sets width and height of display in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). *width* can range from 10 to 200 units, *height* from 5 to 200 units. Default width is 50, default height is determined by the numeric readout font size. |
| <span class="table-cell-nowrap">title = *titleStr*</span> | Sets title of display to the specified string expression. The title appears to the left of the display. If this title is too long, it won't leave enough room to display either the bar or the numeric readout! Defaults to "" (no title). |
|  | Using escape codes you can change the font, size, style and color of the title. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details. |
| <span class="table-cell-nowrap">value = *valExpr*</span> | *valExpr* is the numeric expression to display. It is not a string. |
|  | As of version 6.1, you can use the syntax _NUM:*num* to specify a numeric value without using a dependency. |
| <span class="table-cell-nowrap">valueColor = (*r*,*g*,*b*[,*a*])</span> | Sets the color of the value readout text, if any. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
| <span class="table-cell-nowrap">valueBackColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the background color under the value readout text. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">valueBackColor = 0</span> | Sets the background color under the value readout text to the default color, the standard document background color used on the current operating system, which is usually white. |
| <span class="table-cell-nowrap">win = *winName*</span> | Specifies which window or subwindow contains the named control. If not given, then the top-most graph or panel window or subwindow is assumed. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">zeroColor = (*r*,*g*,*b*[,*a*])</span> | Governs the LED color (in LED mode only). *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). Used in conjunction with the limits keyword such that zeroColor determines one endpoint color when *base* is between *low* and *high*, or LED color when the value is less than *low*. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}

|  |
| --- |
| The target window must be a graph or panel. |

The appearance of the ValDisplay control depends primarily on the *width* and *valwidth* parameters and the width of the title. Space for the individual elements is allocated from left to right, with the title receiving first priority. If the control width hasn't all been used by the title, then the value display gets either *valwidth* [control panel units](/igorpro/user-interface/controls.md#control-panel-units) of room, or what is left. If the control width hasn't been used up, the bar is displayed in the remaining control width:

<img src="Images/ValDisplay/ValDisplay_1.png" width="100%"/>

If you use the bodyWidth keyword, the value readout width and bar width occupy the body width. The total control width is then bodyWidth+title width, and the width from the size keyword is ignored.

The limits values *low*, *high* and *base* and the value of *valExpr* control how the bar, if any, is drawn. The bar is drawn from a starting position corresponding to the *base* value to an ending position determined by the value of *valExpr*, *low* and *high*. *low* corresponds to the left side of the bar, and *high* corresponds to the right. The position that corresponds to the *base* value is linearly interpolated between *low* and *high*.

For example, with *low* = -10, *high* =10, and *base* = 0, a *valExpr* value of 5 will draw from the center of the bar area (0 is centered between -10 and 10) to the right, halfway from the center to the right of the bar area (5 is halfway from 0 to 10):

<img src="Images/ValDisplay/ValDisplay_3.png" width="100%"/>

The *valExpr* must be executable at any time. The expression is stored and executed when the ValDisplay needs to be updated. However, execution will occur outside the routine that creates the ValDisplay, so you must not use local variables in the expression.

*valExpr* may be enclosed in quotes and preceded with a # character (see [When Dependencies are Updated](/igorpro/programming/dependencies.md#when-dependencies-are-updated)) to defer evaluation of the validity of the numeric expression, which may be needed if the expression references as-yet-nonexistent global variables or user-defined functions:


```igor
ValDisplay valdisp0 value=notAVar*2     // "unknown name or symbol" error
ValDisplay valdisp0 value=#"notAVar*2"  // still not valid, no error
Variable notAVar=3                      // now valid; ValDisplay works
```

In a ValDisplay, the #"" syntax permits use of a string expression. Normally, the # prefix signifies that the following text must be a literal quoted string. String expressions are evaluated at runtime to obtain the final expression for the ValDisplay. In other words, there is a level of indirection.

### *Examples* {#examples}
Here is a sampling of some of the forms that ValDisplay controls can take on.

<img src="Images/ValDisplay/ValDisplay_4.png" width="100%"/>

You can use a ValDisplay to replace the bar mode with a solid color fill designed to look like an LED. Use the mode keyword with mode=1 to create an oval LED or mode=2 to create a rectangular LED. You can specify different frames with the rectangular LED but only a simple frame is available for the oval mode. Use mode=0 to revert to bar mode.

The color and brightness of the LED depends on the value that the ValDisplay is monitoring combined with the limits={*low*, *high*, *base*) setting, the two color settings used in bar mode along with a third color (zeroColor) that is used only in LED mode. When the value is between *low* and *high*, the color is a linear combination of endpoint colors. If *base* is between *low* and *high*, the endpoint colors are the low color and the zero color, or the zero color and the high color. For values outside the limits, the appropriate limiting color is chosen.

If *base* is less than the *low* , the endpoint colors are the low color and the high color. In this case, if the value is less than *low* the LED takes on the zero color.

You should use the bodyWidth setting in conjunction with LED mode to keep the LED from dramatically changing size or disappearing when the title is changed.

Try the ValDisplay Demo example experiment to see these different modes in action. The experiment file is in your Igor Pro folder on your hard disk, in the "Examples:Feature Demos" subfolder.

### *See Also* {#see-also}
[Creating ValDisplay Controls](/igorpro/user-interface/controls.md#creating-valdisplay-controls) for more examples.

[printf](/igorpro/commands/printf.md) for an explanation of *formatStr*.

[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.

[Control Panel Units](/igorpro/user-interface/controls.md#control-panel-units) for a discussion of the units used for controls.

The [ControlInfo](/igorpro/commands/controlinfo.md) operation for information about the control.

The [GetUserData](/igorpro/commands/getuserdata.md) function for retrieving named user data.

[Progress Windows](/igorpro/programming/interacting-with-the-user.md#progress-windows) for an example of candy stripe mode=4.

### *Demos* {#demos}
[Open ValDisplay Demo](#igor-pxp/Examples/Feature__Demos/ValDisplay__Demo.pxp)