---
description: "The Chart operation creates or modifies a chart control. Charts are generally used in conjunction with data acquisition."
slug: /commands/chart
---

<div className="command-signature">

## <strong>Chart</strong>  <em>ctrlName</em> [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#chart}

</div>

The Chart operation creates or modifies a chart control. Charts are generally used in conjunction with data acquisition. Charts do not have to be connected to a FIFO, but they are not useful until they are.

For information about the state or status of the control, use the [ControlInfo](/igorpro/commands/controlinfo.md) operation.

### *Parameters* {#parameters}
*ctrlName*  is the name of the Chart to be created or changed.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">align = *alignment*</span> | Sets the alignment mode of the control. The alignment mode controls the interpretation of the *leftOrRight* parameter to the pos keyword. The align keyword was added in Igor Pro 8.00. |
|  | If *alignment*=0 (default), *leftOrRight* specifies the position of the left end of the control and the left end position remains fixed if the control size is changed. |
|  | If *alignment*=1, *leftOrRight* specifies the position of the right end of the control and the right end position remains fixed if the control size is changed. |
| <span class="table-cell-nowrap">chans = {*ch#*, *ch#*,...}</span> | List of FIFO channel numbers that Chart is to monitor. |
| <span class="table-cell-nowrap">color(*ch#* ) = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the color of the specified trace. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">ctab = *colortableName*</span> | When a channel is connected to an image strip FIFO channel, the data is displayed as an image using this built-in color table. Valid names are the same as used in images. Invalid name will result in the default Grays color table being used. |
| <span class="table-cell-nowrap">disable = *d*</span> | Sets user editability of the control. |
|  |<table class="nested-table"><tbody><tr><td>*d*=0:</td><td>Normal.</td></tr><tr><td>*d*=1:</td><td>Hide.</td></tr><tr><td>*d*=2:</td><td>Disable user input. Charts do not change appearance because they are read-only. When disabled, the hand cursor is not shown.</td></tr><tr><td>*d*=3:</td><td>Hide and disable the control. This is useful to disable a control that is also hidden because it is in a hidden tab.</td></tr></tbody></table>
| <span class="table-cell-nowrap">fbkRGB = (*r*,*g*,*b*[,*a*])</span> | Sets frame background color. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">fgRGB = (*r*,*g*,*b*[,*a*])</span> | Sets foreground color (text etc.). *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">fifo = *FIFOName*</span> | Sets FIFO that chart will monitor. |
| <span class="table-cell-nowrap">font = "*fontName*"</span> | Sets chart's font, e.g., font="Helvetica". |
| <span class="table-cell-nowrap">fsize = *s*</span> | Sets font size for chart. |
| <span class="table-cell-nowrap">fstyle = *fs*</span> | Specifies the font style. *fs*  is a bitwise parameter with each bit controlling one aspect of the font style as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">gain(*ch#* ) = *g*</span> | Sets the display gain of the specified channel relative to nominal. Values greater than unity expand the display. |
| <span class="table-cell-nowrap">gridRGB = (*r*,*g*,*b*[,*a*])</span> | Sets grid color. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">guides = {*left, hcenter, right, top, vcenter, bottom*}</span> |  |
|  | Controls attachments of anchor points to layout guides. See [Laying Out Controls in Guides Mode](/igorpro/user-interface/controls.md#laying-out-controls-in-guides-mode) for detailed information and examples. |
|  | Each of *left, hcenter, right, top, vcenter, bottom* is replaced with the name of a layout guide of appropriate orientation. That is, *left, hcenter, right* indicate attachments to vertical guides, and *top, vcenter, bottom* indicate attachments to horizontal guides. Use the special name *kwNone* to represent an unattached anchor point. |
|  | An error results if you overconstrain a control's layout. Of the three horizontal or vertical anchor points, at most two may be attached to layout guides. Attaching one of the three causes a control to move as the layout guide moves. Attaching two causes a control to both move and resize.  Thus, the name *kwNone* will appear at least twice. |
|  | Using *kwNone* for all anchor points results in completely detaching a control from the layout guides. |
| <span class="table-cell-nowrap">help = {*helpStr* }</span> | Sets the help for the control. |
|  | *helpStr* is limited to 1970 bytes (255 in Igor Pro 8 and before). |
|  | You can insert a line break by putting "\r" in a quoted string. |
| <span class="table-cell-nowrap">jumpTo = *p*</span> | Chart jumps to point number *p*. This works in review mode only. |
| <span class="table-cell-nowrap">lineMode(*ch#* ) = *lm*</span> | Set the display line mode for the given channel. |
|  |<table class="nested-table"><tbody><tr><td>*lm*&nbsp;=0:</td><td>Dots mode. Draws values as dots. However, if the number of dots in a strip exceeds maxDots then Igor draws a vertical line from the min to the max of the values packed into the strip.</td></tr><tr><td>*lm*&nbsp;=1:</td><td>Lines mode. Draws a vertical line encompassing the min and the max of the points in a given strip along with the last point of the preceding strip. Since which strip is the preceding strip depends on the direction of motion then the appearance may slightly shift depending on which direction the chart is moving.</td></tr><tr><td>*lm*&nbsp;=2:</td><td>Sticks to zero mode. Draws a vertical line encompassing the min and the max of the points in a given strip along with a value of zero.</td></tr></tbody></table>
| <span class="table-cell-nowrap">mass = *m*</span> | Sets the feel of the chart paper when you move it with the mouse. The larger the mass *m*, the slower the chart recorder responds. Odd values cause the movement of the paper to stop the instant the mouse is clicked while even values continue with the illusion of mass. |
| <span class="table-cell-nowrap">maxDots = *md*</span> | Controls whether points in a given vertical strip of the chart are displayed as dots or as a solid line. See lineMode above. Default is 20. |
| <span class="table-cell-nowrap">offset(*ch#* ) = *o*</span> | Sets the display offset of the specified channel. The offset value is subtracted from the data before the gain is applied. |
| <span class="table-cell-nowrap">oMode = *om*</span> | Chart operation mode. |
|  |<table class="nested-table"><tbody><tr><td>*om*&nbsp;=0:</td><td>Live mode.</td></tr><tr><td>*om*&nbsp;=1:</td><td>Review mode.</td></tr></tbody></table>
| <span class="table-cell-nowrap">pbkRGB = (*r*,*g*,*b*[,*a*])</span> | Sets plot area background color. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">pos = {*leftOrRight*,*top* }</span> | Sets the position in [control panel units](/igorpro/user-interface/controls.md#control-panel-units) of the top/left corner of the control if its alignment mode is 0 or the top/right corner of the control if its alignment mode is 1. See the align keyword above for details. |
| <span class="table-cell-nowrap">ppStrip = *pps*</span> | Number of data points packed into each vertical strip of the chart. |
| <span class="table-cell-nowrap">rename = *newName*</span> | Gives the control a new name. |
| <span class="table-cell-nowrap">rSize(*ch#* ) = *rs*</span> | Sets the relative vertical size allocated to the given channel. Nominal is unity. If the value of *rs*  is zero then this channel shares space with the previous channel. |
| <span class="table-cell-nowrap">sMode = *sm*</span> | Status line mode. |
|  |<table class="nested-table"><tbody><tr><td>*sm*&nbsp;=0:</td><td>Turns off fancy status line and positioning bar.</td></tr><tr><td>*sm*&nbsp;=1:</td><td>Normal mode.</td></tr><tr><td>*sm*&nbsp;=2:</td><td>Uses alternate style for bar.</td></tr></tbody></table>
| <span class="table-cell-nowrap">sRate = *sr*</span> | *sr* is the scroll rate (vertical strips/second). If the chart recorder is in review mode negative numbers scroll in reverse. |
| <span class="table-cell-nowrap">title = *titleStr*</span> | Specifies the chart title. Use "" for no title. |
| <span class="table-cell-nowrap">uMode = *um*</span> | Update mode. |
|  |<table class="nested-table"><tbody><tr><td>*um*&nbsp;=1:</td><td>Fast update with no bells and whistles.</td></tr><tr><td>*um*&nbsp;=2:</td><td>Status line and positioning bar.</td></tr><tr><td>*um*&nbsp;=3:</td><td>Status line, positioning bar, and animated pens.</td></tr></tbody></table>
| <span class="table-cell-nowrap">win = *winName*</span> | Specifies which window or subwindow contains the named control. If not given, then the top-most graph or panel window or subwindow is assumed. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
The target window must be a graph or panel.

The action of some of the Chart keywords depends on whether or not data acquisition is taking place. If the chart is in review mode then all keywords cause the chart to be redrawn. If data acquisition is taking place and the chart is in live mode, some keywords affect new data but do not attempt to update the part of the "paper" that has already been drawn. The following keywords affect only new data during live mode:


```igor
ppStrip, maxDots, gain, offset, color, lineMode
```



### *See Also* {#see-also}
[FIFOs and Charts](/igorpro/advanced-topics.md#fifos-and-charts)

[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.

[Control Panel Units](/igorpro/user-interface/controls.md#control-panel-units) for a discussion of the units used for controls.

The [ControlInfo](/igorpro/commands/controlinfo.md) operation for information about the control.

The [GetUserData](/igorpro/commands/getuserdata.md) function for retrieving named user data.

### *Demos* {#demos}
[Open FIFO Chart Demo](#igor-pxp/Examples/Feature__Demos/FIFO__Chart__Demo__FM.pxp)

[Open Wave Review Chart Demo](#igor-pxp/Examples/Feature__Demos/Wave__Review__Chart__Demo.pxp)

[Open Image Strip FIFO Demo](#igor-pxp/Examples/Imaging/Image__Strip__FIFO__Demo.pxp)