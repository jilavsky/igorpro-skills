---
description: "The Cursor operation moves the cursor specified by cursorName onto the named trace at the point whose X value is x_value or the coordinates of an image pixel…"
slug: /commands/cursor
---

<div className="command-signature overload">

## <strong>Cursor</strong>  [<em>flags</em>] <em>cursorName</em> <em>traceName</em> <em>x_value</em> {#cursor}

</div>
<div className="command-signature overload">

## <strong>Cursor</strong>  [<em>flags</em>] <em>cursorName</em> <em>traceName</em> <em>x_value</em>, <em>y_value</em> {#cursor}

</div>
<div className="command-signature overload">

## <strong>Cursor</strong>  /K [/W=<em>graphName</em> ] <em>cursorName</em> {#cursor}

</div>
<div className="command-signature overload">

## <strong>Cursor</strong>  /I [/F] [<em>flags</em>] <em>cursorName</em> <em>image_name</em> <em>x_value</em>, <em>y_value</em> {#cursor}

</div>
<div className="command-signature">

## <strong>Cursor</strong>  /M [flags] <em>cursorName</em> {#cursor}

</div>

The Cursor operation moves the cursor specified by *cursorName*  onto the named trace at the point whose X value is *x_value*  or the coordinates of an image pixel or free cursor position at *x_value*  and *y_value* .

### *Parameters* {#parameters}
*cursorName*  is one of ten cursors A through J.

### *Flags* {#flags}

|  |  |
| --- | --- |
| /A=*a* |<table class="nested-table"><tbody><tr><td>*a*&nbsp;=0:</td><td>Deactivates the cursor.</td></tr><tr><td>*a*&nbsp;=1:</td><td>Activates the cursor.</td></tr></tbody></table>
|  | Active cursors move with arrow keys or the cursor panel. |
| <span class="table-cell-nowrap">/C = (*r*,*g*,*b,[a]* )</span> | Sets the cursor color. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
| <span class="table-cell-nowrap">/DF = *format*</span> | Sets the format to use when displaying date/time data in the Graph Info Panel (see [Info Panel and Cursors](/igorpro/graphing/graphs.md#info-panel-and-cursors)). |
|  | The /DF flag was added in Igor Pro 9.00. |
|  | The values for *format* are: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Compact format: YYMMDD HHMM.</td></tr><tr><td>1:</td><td>Compact format with seconds added: YYMMDD HHMMSS. The seconds portion may optionally show fractions of seconds - see the /SDGT flag below.</td></tr><tr><td>2:</td><td>Date and Time using a more readable format, the same format you get on a graph axis if you select the &quot;short date&quot; format. Time is formatted as HH\:mm.</td></tr><tr><td>3:</td><td>Date and Time with seconds added. Time is formatted as HH\:mm\:ss. The seconds portion may optionally show fractions of seconds - see the /SDGT flag below.</td></tr><tr><td>4:</td><td>Time without the date. Time is formatted as HH\:mm\:ss. May optionally show fractions of seconds - see the /SDGT flag below.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/DGTS = *nd*</span> | Sets the number of digits precision to use when a cursor value is displayed in the Graph Info Panel (see [Info Panel and Cursors](/igorpro/graphing/graphs.md#info-panel-and-cursors)). The number of digits is set by *nd* and must be a value from 1 to 15. |
|  | The /DGTS flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/F</span> | Allows cursor to roam free. The trace or image provides the axis pair that defines x and y coordinates for the setting and readout. Use /P to set in relative coordinates, where 0,0 is the top left corner of the rectangle defined by the axes and 1,1 is the right bottom corner. |
|  | The fundamental coordinates for a free cursor are plot relative; the ability to use a trace or image is just a convenient way to find the axes for the readout coordinates.
| <span class="table-cell-nowrap">/H = *h*</span> | Specifies crosshairs on cursors. |
|  |<table class="nested-table"><tbody><tr><td>*h*&nbsp;=0:</td><td>Full crosshairs off.</td></tr><tr><td>*h*&nbsp;=1:</td><td>Full crosshairs on.</td></tr><tr><td>*h*&nbsp;=2:</td><td>Vertical hairline.</td></tr><tr><td>*h*&nbsp;=3:</td><td>Horizontal hairline.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/I</span> | Place cursor on specified image. |
| <span class="table-cell-nowrap">/K</span> | Removes the named cursor from the top graph. |
| <span class="table-cell-nowrap">/L = *lStyle*</span> | Line style for crosshairs (full or small). |
|  |<table class="nested-table"><tbody><tr><td>*lStyle*&nbsp;=0:</td><td>Solid lines.</td></tr><tr><td>*lStyle*&nbsp;=1:</td><td>Alternating color dash.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/M</span> | Modifies properties without need to specify trace or image coordinates. Does not work with the /F or /I flags. |
| <span class="table-cell-nowrap">/N = *noKill*</span> | Determines if the cursor is removed ("killed") if the user drags it outside of the plot area: |
|  |<table class="nested-table"><tbody><tr><td>*noKill*&nbsp;=0:</td><td>Remove the cursor (default)</td></tr><tr><td>*noKill*&nbsp;=1:</td><td>Do not remove the cursor</td></tr></tbody></table>
| <span class="table-cell-nowrap">/NUML = *n*</span> | Used in conjunction with /H when *h* is non-zero. Sets the number of crosshair lines to draw. *n* must be between 1 and 3. When *n* is greater than 1, the line separation is set by the /T=*t* flag. If *n* = 2 or 3 and *t* is less than 3, the line appears as if *n* is 1. If *n* = 3 and *t* is less than 5, the appearance reverts to *n* = 2. Lines are symmetrically disposed around the cursor position. When *n* = 3, *t* sets the separation of the outer pair of lines. |
|  | /NUML was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/P</span> | Interprets *x_value* as a point number rather than as an X value. If the cursor is on a trace representing a subrange of a wave, the point numbers are "trace" point numbers. See **Details** below. |
|  | When used with the /I flag, *x_value* and *y_value* are row and column numbers. |
|  | When used with the /F flag, *x_value* and *y_value* are relative graph coordinates (0-1). |
| <span class="table-cell-nowrap">/S = *s*</span> | Sets cursor style. |
|  |<table class="nested-table"><tbody><tr><td>*s*&nbsp;=0:</td><td>Original square or circle.</td></tr><tr><td>*s*&nbsp;=1:</td><td>Small crosshair with letter.</td></tr><tr><td>*s*&nbsp;=2:</td><td>Small crosshair without letter.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/SDGT = *nd*</span> | Set the number of places to the right of the decimal point to be displayed in the Graph Info Panel (see [Info Panel and Cursors](/igorpro/graphing/graphs.md#info-panel-and-cursors)) when the display is in one of the date/time modes that includes seconds, or if the corresponding axis is showing elapsed time. *nd* is a value from 0 to 6. |
|  | The /SDGT flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/T = *t*</span> | Sets the thickness of crosshair lines for /H when *h*  is non-zero. If /NUML sets the number of lines greater than 1 then /T sets the separation of the outer pair of lines. |
|  | *t* is the line thickness or separation distance in units of pixels. The default is /T=1. |
|  | The form /T={*mode* , *t1* , *t2* } provides finer control. |
|  | /T was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/T = {*mode* , *t1* , *t2* }</span> | Sets the thickness of crosshair lines for /H when *h*  is non-zero. If /NUML sets the number of lines greater than 1 then /T sets the separation of the outer pair of lines. |
|  | If *mode* =1 then *t1*  and *t2*  are in units of screen pixels. *t1*  is the vertical line thickness or separation distance and *t2*  is the horizontal line thickness or separation distance. |
|  | The default crosshair appearance is equivalent to /T={1,1,1}. |
|  | If *mode* =0 then *t1*  and *t2*  are in units of axis coordinates and consequently track changes in axis range and graph size. Normally *t1*  is the vertical line thickness or separation distance and *t2*  is the horizontal line thickness or separation distance but they are swapped if the trace or graph is in swap XY mode. |
|  | /T was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/W = *graphName*</span> | Specifies the name of a particular graph window or subwindow. When omitted, action will affect the active window or subwindow |
|  | When identifying a subwindow with *graphName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
Usually *traceName* is the same as the name of the wave displayed by that trace, but it could be a name in instance notation. See [ModifyGraph](/igorpro/commands/modifygraph.md) for a discussion of trace names and instance notation.

A string containing *traceName* can be used with the $ operator to specify *traceName*.

*x_value*  is an X value in terms of the X scaling of the wave displayed by*traceName*. If *traceName*  is graphed as an XY pair, then *x_value*  is not the same as the X axis coordinate. Since the X scaling is ignored when displaying an XY pair in a graph, we recommend you use the /P flag and use a point number for *x_value*.


|  |
| --- |
| *cursorName*  is a name, not a string. |

To get a cursor readout, choose ShowInfo from the Graph menu.

If a cursor is attached to a trace that represents a subrange of a wave, the /P flag causes *x_value* to be interpreted as a trace point number, not as a wave point number. For instance, if the trace was created by the command


```igor
Display yWave[4,25;3]
```

then *x_value*=0 references trace point 0 which corresponds to wave point 4, and *x_value*=1 references trace point 1 which corresponds to wave point 7.

Moving a cursor in a macro or function does not immediately erase the old cursor. DoUpdate has to be explicitly called.

### *Examples* {#examples}

```igor
AppendToGraph myWave                // X coordinates from X scaling of myWave
Cursor A, myWave, leftx(myWave)     // cursor A on first point of myWave

AppendToGraph yWave vs xWave        // X coordinates from xWave, not X scaling
Cursor/P B, yWave,numpnts(yWave)-1  // cursor B on last point of yWave
DoUpdate                            // erase any old A or B cursors
```

### *See Also* {#see-also}
[Programming With Cursors](/igorpro/graphing/graphs.md#programming-with-cursors), [DoUpdate](/igorpro/commands/doupdate.md)