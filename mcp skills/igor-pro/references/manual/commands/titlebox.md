---
description: "The TitleBox operation creates the named title box in the target window."
slug: /commands/titlebox
---

<div className="command-signature">

## <strong>TitleBox</strong>  [/Z] <em>ctrlname</em>  [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#titlebox}

</div>

The TitleBox operation creates the named title box in the target window.

For information about the state or status of the control, use the [ControlInfo](/igorpro/commands/controlinfo.md) operation.

### *Parameters* {#parameters}
*ctrlName*  is the name of the TitleBox control to be created or changed.

The following keyword=value parameters are supported:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">align = *alignment*</span> | Sets the alignment mode of the control. The alignment mode controls the interpretation of the *leftOrRight* parameter to the pos keyword. The align keyword was added in Igor Pro 8.00. |
|  | If *alignment*=0 (default), *leftOrRight* specifies the position of the left end of the control and the position of the control depends on the anchor keyword. |
|  | If *alignment*=1, *leftOrRight* specifies the position of the right end of the control and the right end position remains fixed if the control size is changed. |
|  | There is a conflict between the align keyword and the anchor keyword. See ***TitleBox Positioning*** below. |
| <span class="table-cell-nowrap">anchor = *hv*</span> | Specifies the anchor mode a two letter code, *hv*. *h*  may be L, M or R for left, middle, and right. *v*  may be T, C or B for top, center and bottom. Default is LT. |
|  | If *fixedSize*=1, the anchor code sets the positioning of text within the frame. |
| <span class="table-cell-nowrap">appearance = {*kind*  [, *platform* ]}</span> |  |
|  | Sets the appearance of the control. *platform*  is optional. Both parameters are names, not strings. |
|  | *kind*  can be one of `default`, `native`, or `os9`. |
|  | *platform*  can be one of `Mac`, `Win`, or `All`. |
|  | See [Button](/igorpro/commands/button.md) and [DefaultGUIControls](/igorpro/commands/defaultguicontrols.md) for more appearance details. |
| <span class="table-cell-nowrap">disable = *d*</span> | Sets user editability of the control. |
|  |<table class="nested-table"><tbody><tr><td>*d*=0:</td><td>Normal.</td></tr><tr><td>*d*=1:</td><td>Hide.</td></tr><tr><td>*d*=2:</td><td>Draw in gray state.</td></tr></tbody></table>
| <span class="table-cell-nowrap">fColor = (*r*,*g*,*b*[,*a*])</span> | Sets color of the font. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| fixedSize=*f* |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>The titlebox automatically sizes itself to fit the title text (default).</td></tr><tr><td>*f*&nbsp;=1:</td><td>The size settings are honored, and the titlebox does not automatically size itself to fit the title text.</td></tr></tbody></table>
| <span class="table-cell-nowrap">font = "*fontName*"</span> | Sets the font used for the control, e.g., font="Helvetica". |
| <span class="table-cell-nowrap">frame = *f*</span> | Sets frame style. |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>No frame</td></tr><tr><td>*f*&nbsp;=1:</td><td>Default (same as *f* =3)</td></tr><tr><td>*f*&nbsp;=2:</td><td>Simple box.</td></tr><tr><td>*f*&nbsp;=3:</td><td>3D sunken frame.</td></tr><tr><td>*f*&nbsp;=4:</td><td>3D raised frame.</td></tr><tr><td>*f*&nbsp;=5:</td><td>Text well.</td></tr></tbody></table>
| <span class="table-cell-nowrap">fsize = *s*</span> | Sets font size. |
| <span class="table-cell-nowrap">fstyle = *fs*</span> | *fs*  is a bitwise parameter with each bit controlling one aspect of the font style as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">guides = {*left, hcenter, right, top, vcenter, bottom*}</span> |  |
|  | Controls attachments of anchor points to layout guides. See [Laying Out Controls in Guides Mode](/igorpro/user-interface/controls.md#laying-out-controls-in-guides-mode) for detailed information and examples. |
|  | Each of *left, hcenter, right, top, vcenter, bottom* is replaced with the name of a layout guide of appropriate orientation. That is, *left, hcenter, right* indicate attachments to vertical guides, and *top, vcenter, bottom* indicate attachments to horizontal guides. Use the special name *kwNone* to represent an unattached anchor point. |
|  | An error results if you overconstrain a control's layout. Of the three horizontal or vertical anchor points, at most two may be attached to layout guides. Attaching one of the three causes a control to move as the layout guide moves. Attaching two causes a control to both move and resize.  Because of limits on constraints, the name *kwNone* will appear at least twice. |
|  | If you set *fixedSize*=1, the control can be arbitrarily resized, allowing two attachments in each direction. If *fixedSize*=0, the controls width and height are set by the size of the enclosed text. In that case, only one guide can be attached in each direction. That means the guides can move the control but not change its size. |
| <span class="table-cell-nowrap">help = {*helpStr* }</span> | Sets the help for the control. |
|  | *helpStr* is limited to 1970 bytes (255 in Igor Pro 8 and before). |
|  | You can insert a line break by putting "\\r" in a quoted string. |
| <span class="table-cell-nowrap">labelBack = (*r*,*g*,*b*[,*a*]) or 0</span> |  |
|  | Sets background color for title box. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). If not set (or labelBack=0), then background is transparent (not erased). |
| <span class="table-cell-nowrap">pos = {*leftOrRight*,*top* }</span> | Sets the position in [control panel units](/igorpro/user-interface/controls.md#control-panel-units) of the top/left or top/right corner of the control at the time it is created. Unless *fixedSize*=1, a TitleBox control adjusts its size to fit the title text and the position can move in a way that depends on the anchor and align modes. See **TitleBox Positioning** below. |
| <span class="table-cell-nowrap">pos+ = {*dx,dy*}</span> | Offsets the position of the control in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">size = {*w*,*h*}</span> | Set the width and height in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
|  | If *fixedSize*=1, sets the width of the control. If *fixedSize*=0, a TitleBox control adjusts its size to the title text, resulting in confusion about what the size does. In this case, size={0,0} is recommended. See ***TitleBox Positioning*** below. |
| <span class="table-cell-nowrap">title = *titleStr*</span> | Sets the text of the title box to *titleStr*. *titleStr*  is limited to 255 bytes. |
|  | Using escape codes you can change the font, size, style and color of the title. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details. |
| <span class="table-cell-nowrap">variable = *svar*</span> | Specifies an optional global string variable from which to get the TitleBox text. |
| <span class="table-cell-nowrap">win = *winName*</span> | Specifies which window or subwindow contains the named control. If not given, then the top-most graph or panel window or subwindow is assumed. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The text can come from either the title=*titleStr*  or variable=*svar*  method. Whichever is used last is the current method. The maximum length of text with the title=*titleStr*  method is 255 bytes while the variable=*svar*  method has no limit.

Using escape codes you can change the font, size, style and color of text, and apply other effects. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details.

By default, the titlebox automatically resizes itself relative to the anchor point on the rectangle that encloses the text. Therefore you can specify a size of 0,0 along with a pos value in order to place the anchor point at the desired position. When fixedSize=1 is used, the titlebox does not resize itself and instead honors the values specified via the size keyword.

TitleBoxes can be used not only for titles but also as status or results readout areas, especially in conjunction with the variable= *svar* mode. When using a titlebox like this, you may find it useful to use fixedSize=1 so that the titlebox doesn't change size as the text changes.

### *TitleBox Positioning* {#titlebox-positioning}
For compatibility with other controls, you can use the align=1 to maintain the position of the right end of a TitleBox control. This presents a conflict with the anchor keyword. To resolve the conflict, these rules are applied:

Applying align=1, which sets the alignment mode to right alignment, overrides any horizontal positioning specified using the anchor keyword.

Applying the anchor keyword resets the alignment mode to 0 and the anchor mode controls the horizontal position of the control.

If you specify fixedSize=1, only the align and pos keywords affect horizontal positioning; the anchor keyword has no effect.

For clarity, don't mix the anchor and align keywords unless you are using fixedSize=1. Use anchor in preference to align unless you are trying to keep the right ends of various types of controls aligned, especially on high-resolution displays on Windows.

### *Examples* {#examples}

```igor
NewPanel /W=(94,72,459,294)
DrawLine 150,32,150,140
DrawLine 70,100,213,100	// draw crossing lines at 150,100

// illustrate a default box
TitleBox tb1,title="A title box\rwith 2 lines",pos={150,100}

// Move center to 150,100
TitleBox tb1,pos={150,100},size={0,0},anchor=MC

// Set background color and therfore opaque mode
TitleBox tb1,labelBack=(55000,55000,65000)

// Now a few frame styles. Run these one at a time
TitleBox tb1,frame= 0	// no frame
TitleBox tb1,frame= 2	// plain frame
TitleBox tb1,frame= 3	// 3D sunken
TitleBox tb1,frame= 4	// 3D raised
TitleBox tb1,frame= 5	// text well

// Now some fancy text..
TitleBox tb1,frame= 1	// back to default (3D raised)
TitleBox tb1,title= "\Z18\[020 log\\B10\\M|[1 + 2K(jwt) + (jwt)\\S2\\M]|\\S-1"

// Create a string variable and hook up to the TitleBox
String s1= "text from a string variable"
TitleBox tb1,variable=s1

// Change string variable contents and note automatic update of TitleBox
s1= "something new"

// A TitleBox with right end at X=200 because the align keyword takes precedence
TitleBox tb, pos={200,40},size={0,0},align=1,anchor=MT,title="Short Title"

// A TitleBox with right end at X=200 because align by itself overrides any preexisting anchor
TitleBox tb, pos={200,40},size={0,0},align=1,title="Short Title"

// A TitleBox with text centered in the frame and right end at X=200,
// with frame always 75 points wide:
TitleBox tb, pos={200,40},size={75,20},align=1,fixedSize=1,anchor=MT,title="Short Title"
```

### *See Also* {#see-also}

|  |
| --- |
| [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) |

[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.

[Control Panel Units](/igorpro/user-interface/controls.md#control-panel-units) for a discussion of the units used for controls.

The [ControlInfo](/igorpro/commands/controlinfo.md) operation for information about the control.