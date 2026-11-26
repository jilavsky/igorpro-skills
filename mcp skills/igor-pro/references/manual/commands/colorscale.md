---
description: "The ColorScale operation adds a color scale (or \"color legend\") annotation a graph, Gizmo plot or page layout. For background information, see Color Scales."
slug: /commands/colorscale
---

<div className="command-signature">

## <strong>ColorScale</strong>  [<em>flags</em>] [, <em>keyword</em> = <em>value</em>, ...] [<em>axisLabelStr</em> ] {#colorscale}

</div>

The ColorScale operation adds a color scale (or "color legend") annotation a graph, Gizmo plot or page layout. For background information, see [Color Scales](/igorpro/graphing/annotations.md#color-scales).

The ability to add colorscales to a Gizmo plot was added in Igor Pro 8.00.

The ColorScale operation can be executed with no flags and no parameters. It acts on the current target window or the active subwindow or on the window or subwindow specified by the /W flag.

When the target is a graph, the color scale represents the colors and values associated with the first image plot that was added to the graph. If there is no image plot in the graph, the color scale represents the first contour plot or first f(z) trace added to the graph, one of which must exist for the command to execute without error when executed without parameters.

When the target is a Gizmo plot, the color scale represents the colors and values associated with the first surface object, preferring the surface fill color table over the surface gridlines color table. If there is no such surface object, the color scale represents the first scatter object using a color table. If there is no such scatter object, the color scale represents the first path object using a color table. If there is no such path object, the color scale represents the first ribbon object using a color table.

Executing `ColorScale` with no parameters when the target is a page layout displays a color bar as if the ctab={0,100,Rainbow} parameters had been specified.

### *Flags* {#flags}
Use the /W=*win* flag to specify a specific graph or layout window. When used on the command line or in a Macro or Proc, /W must precede all other flags.

To change a color scale, use the /C/N=*name* flags. Annotations are automatically named "text0", "text1", etc if no name is specified when it is created, and you must use that name to modify an existing annotation or else a new one will be created.

For explanations of all flags see [TextBox](/igorpro/commands/textbox.md).

### *Parameters* {#parameters}
The following keyword-value pairs are the important parameters to the ColorScale operation, because they specify what object the color scale is representing.

:::note
For use with page layouts, the keyword ={graphName,...} form is required.
:::

For graphs it is simpler to use the image=imageInstanceName  form (omitting graphName), though you can use $"" to mean the top graph, or specify the name of another graph with the long form. See the examples.

|  |  |
| --- | --- |
| *axisLabelStr* | Contains text that is printed beside the color scale's main axis. This text is interpreted the same way as for the [Label](/igorpro/commands/label.md) operation. |
|  | Using escape codes you can change the font, size, style and color of text, create superscripts and subscripts, and apply other effects. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details. |
|  | You can use the [AppendText](/igorpro/commands/appendtext.md) or [ReplaceText](/igorpro/commands/replacetext.md) operations to modify this axis label string. The default value for axisLabelStr is "". |
| <span class="table-cell-nowrap">cindex = *cindexMatrixWave*</span> |  |
|  | The colors shown are those in the named color index wave with axis values derived from the wave's X (row) scaling and units. |
|  | The image colors are determined by doing a lookup in the specified matrix wave. See the cindex keyword as used in the [ModifyImage](/igorpro/commands/modifyimage.md) operation. |
| <span class="table-cell-nowrap">contour = *contourInstanceName*</span> |  |
| <span class="table-cell-nowrap">contour = {*graphName*,*contourInstanceName* }</span> |  |
|  | The colors show the named contour plot's line colors and associated contour (Z) values and contour data units. All of the image plot's characteristics are represented, including color table, cindex, and fixed colors. |
|  | *graphName* can be just the name of a top-level graph window or a subwindow specification like Panel0#G0. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on subwindow specifications. |
| <span class="table-cell-nowrap">contourFill = *contourInstanceName*</span> |  |
| <span class="table-cell-nowrap">contourFill = {*graphName*,*contourInstanceName* }</span> |  |
|  | The colors show the named contour plot's fill colors and associated contour (Z) values and contour data units. All of the image plot's characteristics are represented, including color table, cindex, and fixed colors. |
|  | *graphName* can be just the name of a top-level graph window or a subwindow specification like Panel0#G0. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on subwindow specifications. |
|  | The contourFill keyword was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">ctab = {*zMin*,*zMax*,*ctName*, *reverse* }</span> |  |
|  | The color table specified by *ctName* is drawn in the color legend. *ctName* can be any of those returned by the [CTabList](/igorpro/commands/ctablist.md) function, such as Grays or Rainbow. Also see [Color Tables](/igorpro/graphing/contour-plots.md#color-tables). |
|  | The color table name can be omitted if you want to leave it unchanged. *zMin* and *zMax* set the range of Z values to map. Set parameter *mode* to 1 to reverse the color table;  zero or missing value does not reverse the color table. |
|  | The color table specified by *ctName* is drawn in the color legend. |
|  | *zMin* and *zMax* set the range of Z values to map. |
|  | The color table name can be omitted if you want to leave it unchanged. |
|  | *ctName* can be any color table name returned by the [CTabList](/igorpro/commands/ctablist.md) function, such as Grays or Rainbow (see [Color Tables](/igorpro/graphing/contour-plots.md#color-tables)) or the name of a 3 column or 4 column color table wave (see [Color Table Waves](/igorpro/graphing/image-plots.md#color-table-waves)). |
|  | A color table wave name supplied to ctab must not be the name of a built-in color table (see [CTabList](/igorpro/commands/ctablist.md)). A 3 column or 4 column color table wave must have values that range between 0 and 65535. Column 0 is red, 1 is green, and 2 is blue. In column 3 a value of 65535 is fully opaque and 0 is fully transparent. |
|  | Set *reverse* to 1 to reverse the color table. Setting it to 0 or omitting it leaves the color table order unreversed. |
| <span class="table-cell-nowrap">image = *imageInstanceName*</span> |  |
| <span class="table-cell-nowrap">image = {*graphName*,*imageInstanceName* }</span> |  |
|  | The colors show the named image plot's colors and associated image (Z) values and image data units. All of the image plot's characteristics are represented, including color table, cindex, lookup wave, eval colors, and NaN transparency. |
|  | <div><Admonition type="note"><p>Only false-color image plots can be used with ColorScale (see [Indexed Color Details](/igorpro/graphing/image-plots.md#indexed-color-details)).</p></Admonition></div> |
|  | *graphName* can be just the name of a top-level graph window or a subwindow specification like `Panel0#G0`. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on subwindow specifications. |
| <span class="table-cell-nowrap">logLabel = *t*</span> | *t* is the maximum number of decades before minor tick labels are suppressed. The default value is 3. |
|  | The logLabel keyword was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">logTicks = *t*</span> | *t*=0 means "auto". This is the default value. |
|  | If *t* is not 0 then it represents the maximum number of decades before minor ticks are suppressed. |
|  | The logTicks keyword was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">lookup = *waveName*</span> | Specifies an optional 1D wave that is used to modify the mapping of scaled z values into the color table specified with the ctab keyword. Values should range from 0.0 to 1.0. A linear ramp from 0 to 1 would have no effect while a ramp from 1 to 0 would reverse the image. Used to apply gamma correction to grayscale images or for special effects. Use lookup=$"" to remove option. |
|  | This keyword is not needed with the image keyword, even if the image plot uses a lookup wave. The image plot's lookup wave is used instead of the ColorScale lookup wave. |
| <span class="table-cell-nowrap">path = *gizmoObjectSpec*</span> |  |
| <span class="table-cell-nowrap">path = {*gizmoName*, *gizmoObjectSpec*}</span> |  |
|  | The colors show the named Gizmo path plot's colors and associated X, Y, or Z values and units. Only the path plot's color table is represented. Other color modes such as color wave or solid colors are not supported. |
|  | *gizmoName* can be just the name of a top-level Gizmo window or a subwindow specification like Panel0#GZ0. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on subwindow specifications. |
|  | *gizmoObjectSpec* can be just the name of the object like path0, or a colon-separated path to the object in a group like group0:path0. Unlike [ModifyGizmo](/igorpro/commands/modifygizmo.md) setCurrentGroup, *gizmoObjectSpec* does not start with the name of the Gizmo window. |
|  | The path keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">ribbon = *gizmoObjectSpec*</span> |  |
| <span class="table-cell-nowrap">ribbon = {*gizmoName*, *gizmoObjectSpec*}</span> |  |
|  | The colors show the named Gizmo ribbon plot's colors and associated X, Y, or Z values and units. Only the ribbon plot's color table is represented. Other color modes such as color wave or solid colors are not supported. |
|  | See the path keyword for {*gizmoName*, *gizmoObjectSpec*} details. |
|  | The ribbon keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">scatter = *gizmoObjectSpec*</span> |  |
| <span class="table-cell-nowrap">scatter = {*gizmoName*, *gizmoObjectSpec*}</span> |  |
|  | The colors show the named Gizmo scatter plot's marker colors and associated X, Y, or Z values and units. Only the scatter plot's color table is represented. Other color modes such as color wave or solid colors are not supported. |
|  | See the path keyword for {*gizmoName*, *gizmoObjectSpec*} details. |
|  | The scatter keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">surface = *gizmoObjectSpec*</span> |  |
| <span class="table-cell-nowrap">surface = {*gizmoName*, *gizmoObjectSpec* }</span> |  |
|  | The colors show the named Gizmo surface plot's grid line colors and associated surface X, Y, or Z values and surface matrix units. Unlike image plots, only the surface plot's color table is represented. Other color modes such as color wave or solid colors are not supported. |
|  | See the path keyword for {*gizmoName*, *gizmoObjectSpec*} details. |
|  | The surface keyword was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">surfaceFill = *gizmoObjectSpec*</span> |  |
| <span class="table-cell-nowrap">surfaceFill = {*gizmoName*, *gizmoObjectSpec* }</span> |  |
|  | The colors show the named Gizmo surface plot's fill colors and associated surface X, Y, or Z values and surface matrix units. Unlike image plots, only the surface plot's color table is represented. Other color modes such as color wave or solid colors are not supported. |
|  | *gizmoName* can be just the name of a top-level Gizmo window or a subwindow specification like Panel0#GZ0. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on subwindow specifications. |
|  | See the path keyword for {*gizmoName*, *gizmoObjectSpec*} details. |
|  | The surfaceFill keyword was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">trace = *traceInstanceName*</span> |  |
| <span class="table-cell-nowrap">trace = {*graphName*,*traceInstanceName* }</span> |  |
|  | The colors show the color(s) of the named trace. This is useful when the trace has its color set by a "z wave" using the [ModifyGraph](/igorpro/commands/modifygraph.md) zColor(traceName)=... feature. In the Modify Trace Appearance dialog this is selected in the "Set as f(z)" subdialog. The color scale's main axis shows the range of values in the z wave, and displays any data units the wave may have. |
|  | *graphName* can be just the name of a top-level graph window or a subwindow specification like Panel0#G0. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on subwindow specifications. |

### *Size Parameters* {#size-parameters}
The following keyword-value parameters modify the size of the color scale annotation. These keywords are similar to those used by the [Slider](/igorpro/commands/slider.md) control. The size of the annotation is indirectly controlled by setting the size of the "color bar" and the various axis parameters. The annotation sizes itself to accommodate the color bar, tick labels, and axis label(s).


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">height = *h*</span> | Sets height of color bar in points, overriding any heightPct setting. The default height is 75% of the plot area height if the color scale is vertical, or a constant of 15 points if the color scale is horizontal. The default is restored by specifying height=0. Specifying a heightPct value resets height to this default. |
| <span class="table-cell-nowrap">heightPct = *hpct*</span> | Sets height as a percentage of graph's plot area, overriding any height setting. The default height is 75% of the plot area height if the color scale is vertical, or a constant of 15 points if the color scale is horizontal. The default height is restored by setting heightPct=0. |
| <span class="table-cell-nowrap">side = *s*</span> | Selects on which axis to draw main axis ticks. |
|  |<table class="nested-table"><tbody><tr><td>*s*&nbsp;=1:</td><td>Right of the color bar if vert=1, or below if vert=0.</td></tr><tr><td>*s*&nbsp;=2:</td><td>Left of the color bar if vert=1, or above if vert=0.</td></tr></tbody></table>
| <span class="table-cell-nowrap">vert = *v*</span> | Specifies orientation of color scale. |
|  |<table class="nested-table"><tbody><tr><td>*v*&nbsp;=0:</td><td>Horizontal.</td></tr><tr><td>*v*&nbsp;=1:</td><td>Vertical (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">width = *w*</span> | Sets width of color bar in points, overriding any widthPct setting. The default width is a constant 15 points if the color scale is vertical, or 75% of the plot area width if the color scale is horizontal. The default is restored by specifying width=0. Specifying a widthPct value resets width to this default. |
| <span class="table-cell-nowrap">widthPct = *wpct*</span> | Sets width as a percentage of graph's plot area, overriding any width setting. The default width is a constant 15 points if the color scale is vertical, or 75% of the plot area width if the color scale is horizontal. The default is restored by setting widthPct=0. Specifying a width value resets widthPct to this default. |

### *Color Bar Parameters* {#color-bar-parameters}
The following keyword-value parameters modify the appearance of the color scale color bar.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">colorBoxesFrame = *on*</span> | Draws frames surrounding up to 99 swatches of colors in the color bar (*on* =1). |
|  | When specifying more than 99 colors in the color bar (such as the Rainbow color table, which has 100 colors), the boxes aren't framed. Framing color boxes is effective only for small numbers of colors. Set the width of the frame with the frame keyword. |
|  | Use *on* =0 to turn off color box frames. |
| <span class="table-cell-nowrap">frame = *f*</span> | Specifies the thickness of the frame drawn around the color bar in points (*f* can range from 0 to 5 points). The default is 1 point. Fractional values are permitted. |
|  | Turn frames off with *f* =0. Values less that 0.5 do not display on screen, but the thin frame will print. |
| <span class="table-cell-nowrap">frameRGB = (*r*,*g*,*b*[,*a*]) or 0</span> |  |
|  | Sets the color of the frame around the color bar. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The frame includes the individual color bar colors when colorBoxesFrame=1. |
|  | The frame will use the colorscale foreground color, as set by the /G flag, when frameRGB=0. |

### *Axis Parameters* {#axis-parameters}
The following keyword-value parameters modify the appearance of the color scale axes. These keywords are based on the [ModifyGraph for Axes](/igorpro/commands/modifygraph.md#modifygraph-for-axes) keywords because they modify the main or secondary color scale axes.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">axisRange = {*zMin*, *zMax* }</span> |  |
|  | Sets the color bar axis range to values specified by *zMin* and *zMax*. Use * to use the default axis range for either or both values. |
|  | Omit *zMin* or *zMax* to leave that end of the range unchanged. For example, use {zMin, } to change *zMin* and leave *zMax* alone, or use { ,*} to set only the axis maximum value to the default value. |
| <span class="table-cell-nowrap">dateInfo = {*sd*,*tm*,*dt* }</span> | Controls formatting of date/time axes. |
|  |<table class="nested-table"><tbody><tr><td>*sd*=0:</td><td>Show date in the date&amp;time format.</td></tr><tr><td></td><td>The date is always suppressed if *tm*=2 (elapsed time).</td></tr><tr><td></td><td>The time is always suppressed if there are fewer than one ticks per day and tm=0 (12-hour time) or tm=1 (24-hour time).</td></tr><tr><td>*sd*=1:</td><td>Suppress date.</td></tr><tr><td></td><td>The date is always suppressed if *tm*=2 (elapsed time).</td></tr><tr><td>*sd*=2:</td><td>Suppress time.</td></tr><tr><td></td><td>The time is always shown if *tm*=2 (elapsed time).</td></tr><tr><td></td><td>*sd*=2 requires Igor Pro 9.00 or later.</td></tr><tr><td>*tm*=0:</td><td>12 hour (AM/PM) time.</td></tr><tr><td>*tm*=1:</td><td>24 hour (military) time.</td></tr><tr><td>*tm*=2:</td><td>Elapsed time.</td></tr><tr><td>*dt*=0:</td><td>Short dates (2/22/90).</td></tr><tr><td>*dt*=1:</td><td>Long dates (Thursday, February 22, 1990).</td></tr><tr><td>*dt*=2:</td><td>Abbreviated dates (Thurs, Feb 22, 1990).</td></tr></tbody></table>
|  | These have no effect unless the axis is controlled by a wave with 'dat' data units. |
|  | These date formats do not work with dates before 0001-01-01 in which case the axis displays an empty string. You can apply custom date formats using the dateFormat keyword in such cases. |
|  | To use a custom date format as specified by the dateFormat keyword, you must specify -1 for the *dt* parameter to dateInfo. |
|  | For an f(z) color scale: |
|  | <code class="igor">SetScale d, 0,0, "dat", fOfZWave</code> |
|  | For a contour plot or image plot color scale: |
|  | <code class="igor">SetScale d, 0,0, "dat", ZorXYZorImageWave</code> |
|  | See [Date/Time Axes](/igorpro/graphing/graphs.md#date-time-axes) and [Date, Time, and Date&Time Units](/igorpro/igor-basics/waves.md#date-time-and-date-time-units) for details on how date/time axes work. |
| <span class="table-cell-nowrap">font = *fontNameStr*</span> | Name of font as string expression. If the font does not exist, the default font is used. Specifying "default" has the same effect. Unlike ModifyGraph, the fontName is evaluated at runtime, and its absence from the system is not an error. |
| <span class="table-cell-nowrap">fsize = *s*</span> | *s* =0: use the default (graph) font size for tick labels and axis label(s). |
|  | *s* is the font size in points. The default is 0 (auto font size). |
| <span class="table-cell-nowrap">fstyle = *fs*</span> | Specifies the font style. *fs* is a bitwise parameter with each bit controlling one aspect of the font style for the tick mark labels as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">highTrip = *h*</span> | If the extrema of an axis are between its lowTrip and its highTrip then tick mark labels use fixed point notation. Otherwise they use exponential (scientific or engineering) notation. The default highTrip is 100,000. |
| <span class="table-cell-nowrap">lblLatPos = *p*</span> | Sets a lateral offset for the main axis label. This is an offset parallel to the axis. p is in points. Positive is down for vertical axes and to the right for horizontal axes. The default is 0. |
| <span class="table-cell-nowrap">lblMargin = *m*</span> | Moves the main axis label by *m* points (default is 0) from the normal position. The default value is -5, which brings the axis label closer to the axis. Use more positive values to move the axis label away from the axis. |
| <span class="table-cell-nowrap">lblRot = *r*</span> | Rotates the main axis label by *r* degrees counterclockwise starting from the normal label orientation. *r* is a value from -360 to 360. |
| <span class="table-cell-nowrap">log = *l*</span> | Specifies the axis type. |
|  |<table class="nested-table"><tbody><tr><td>*l*&nbsp;=0:</td><td>Linear (default).</td></tr><tr><td>*l*&nbsp;=1:</td><td>Log base 10.</td></tr><tr><td>*l*&nbsp;=2:</td><td>Log base 2.</td></tr></tbody></table>
| <span class="table-cell-nowrap">logHTrip = *h*</span> | Same as highTrip but for log axes. The default is 10,000. |
| <span class="table-cell-nowrap">logLTrip = *l*</span> | Same as lowTrip but for log axes. The default is 0.0001. |
| <span class="table-cell-nowrap">logTicks = *t*</span> | *t* is maximum number of decades in log axis before minor ticks are suppressed. |
| <span class="table-cell-nowrap">lowTrip = *l*</span> | If the extrema of an axis are between its lowTrip and its highTrip then tick mark labels use fixed point notation. Otherwise they use exponential (scientific or engineering) notation. The default lowTrip is 0.1. |
| minor=*m* |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Disables minor ticks (default).</td></tr><tr><td>*m*&nbsp;=1:</td><td>Enables minor ticks.</td></tr></tbody></table>
| notation=*n* |<table class="nested-table"><tbody><tr><td>*n*&nbsp;=0:</td><td>Engineering notation (default).</td></tr><tr><td>*n*&nbsp;=1:</td><td>Scientific notation.</td></tr></tbody></table>
| <span class="table-cell-nowrap">nticks = *n*</span> | *n* is the approximate number of ticks to be distributed along the main axis. Ticks are labelled using the same automatic algorithm used for graph axes. The default is 5. |
|  |<table class="nested-table"><tbody><tr><td>*n*&nbsp;=0:</td><td>no ticks.</td></tr></tbody></table>
| <span class="table-cell-nowrap">prescaleExp = *exp*</span> | Multiplies axis range by 10^*exp* for tick labeling and *exp* is subtracted from the axis label exponent. In other words, the exponent is moved from the tick labels to the axis label. The default is 0 (no modification). See the discussion in [ModifyGraph](/igorpro/commands/modifygraph.md)'s Details section. |
| <span class="table-cell-nowrap">tickExp = *te*</span> | *te* =1 forces tick labels to exponential notation when labels have units with a prefix. *te* =0 turns this off. |
| <span class="table-cell-nowrap">tickLen = *t*</span> | Sets the length of the ticks. *t* is the major tick mark length in points. This value must be between -100 and 50. |
|  |<table class="nested-table"><tbody><tr><td>*t*&nbsp;=&nbsp;0&nbsp;to&nbsp;50:</td><td>Draws tick marks between the tick labels and the colors box.</td></tr><tr><td>*t*&nbsp;=-1:</td><td>Auto tick length (default), equal to 70% of the tick label font size. Draws tick marks between the tick labels and the colors box.</td></tr><tr><td>*t*&nbsp;=-2&nbsp;to&nbsp;-50:</td><td>Draws tick marks crossing the edge of the colors box nearest the tick labels. The actual total tick mark length is -*t*.</td></tr><tr><td>*t*&nbsp;=-100&nbsp;to&nbsp;-51:</td><td>Draws tick marks inside the edge of the colors box nearest the tick labels. Actual tick mark length is -(*t* +50). For example, -58 makes an inside tick mark that is 8 points long.</td></tr></tbody></table>
| <span class="table-cell-nowrap">tickThick = *t*</span> | *t* is the tick mark thickness in points (from 0 to 5 points). The default is 1 point. Fractional values are permitted. |
|  | *t* =0 turns tick marks off, but not the tick labels. |
| tickUnit=*tu* |<table class="nested-table"><tbody><tr><td>*tu*&nbsp;=1:</td><td>suppresses units labels attached to tick marks.</td></tr><tr><td>*tu*&nbsp;=0:</td><td>turns units labels back on.</td></tr></tbody></table>
| <span class="table-cell-nowrap">userTicks = {*tvWave*,*tlblWave* }</span> |  |
|  | Supplies user defined tick positions and labels for the main axis. *TvWave* contains the numeric tick positions while text wave *tlblWave* contains the corresponding labels. |
|  | Overrides normal ticking specified by nticks. |
|  | See [User Ticks from Waves](/igorpro/graphing/graphs.md#user-ticks-from-waves) for details. |
|  | The tick mark labels can be multiline and use styled text. For more details, see [Fancy Tick Mark Labels](/igorpro/graphing/category-plots.md#fancy-tick-mark-labels). |
| <span class="table-cell-nowrap">ZisZ = *z*</span> | *z* =1 labels the zero tick mark label (if any) as the single digit "0" regardless of the number of digits used for other labels. Default is *z*=0. |

### *Secondary Axis Parameters* {#secondary-axis-parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">axisLabel2 = *axisLabelString2*</span> |  |
|  | Axis label for the secondary axis. This axis label is drawn only if userTicks2 is in effect. Text after any \r character is ignored, as is the \r character. The default is "". |
| <span class="table-cell-nowrap">lblLatPos2 = *p*</span> | Sets a lateral offset for the secondary axis label. This is an offset parallel to the axis. p is in points. Positive is down for vertical axes and to the right for horizontal axes. The default is 0. |
| <span class="table-cell-nowrap">lblMargin2 = *m*</span> | *m* is distance in points (default 0) to move the secondary axis label from the position that would be normal for a graph. The default is value is -5, which brings the axis label closer to the axis. Use more positive values to move the axis label away from the axis. |
| <span class="table-cell-nowrap">lblRot2 = *r*</span> | Rotates the secondary axis label by *r* degrees counterclockwise starting from the normal label orientation. *r* is a value from -360 to 360. |
| <span class="table-cell-nowrap">userTicks2 = {*tvWave*,*tlblWave* }</span> |  |
|  | Supplies user defined tick positions and labels for a second axis which is always on the opposite side of the color bar from the main axis. The tick mark labels can be multiline and use styled text. For more details, see [Fancy Tick Mark Labels](/igorpro/graphing/category-plots.md#fancy-tick-mark-labels). This is the only way to draw a second axis. |

### *Image Plot ColorScale Example* {#image-plot-colorscale-example}

```igor
Make/O/N=(20,20) img=p*q; NewImage img              // Make and display an image
ColorScale                                          // create default color scale
ColorScale/C/N=text0 nticks=3,minor=1,"Altitude"    // first annotation is text0
ModifyImage img ctab= {*,*,Relief19,0}              // 19-color color table
ColorScale/C/N=text0 axisRange={100,300}            // Detail for 100-300 range
ColorScale/C/N=text0 colorBoxesFrame=1              // Frame the color boxes
ColorScale/C/N=text0 frameRGB=(65535,0,0)           // Red frame
```

### *Gizmo Plot ColorScale Example* {#gizmo-plot-colorscale-example}

```igor
Window GizmoDemo() : GizmoPlot
	PauseUpdate; Silent 1
	// Building Gizmo 7 window...
	NewGizmo/W=(35,45,435,353)
	ModifyGizmo startRecMacro=700
	ModifyGizmo scalingOption=63
	AppendToGizmo Surface=root:img,name=surface0
	ModifyGizmo ModifyObject=surface0,objectType=surface,property={ srcMode,0}
	ModifyGizmo ModifyObject=surface0,objectType=surface,property={ surfaceCTab,CyanMagenta}
	AppendToGizmo Axes=boxAxes,name=axes0
	ModifyGizmo ModifyObject=axes0,objectType=Axes,property={-1,axisScalingMode,1}
	ModifyGizmo ModifyObject=axes0,objectType=Axes,property={-1,axisColor,0,0,0,1}
	ModifyGizmo ModifyObject=axes0,objectType=Axes,property={0,ticks,3}
	ModifyGizmo ModifyObject=axes0,objectType=Axes,property={1,ticks,3}
	ModifyGizmo ModifyObject=axes0,objectType=Axes,property={2,ticks,3}
	ModifyGizmo modifyObject=axes0,objectType=Axes,property={-1,Clipped,0}
	ModifyGizmo setDisplayList=0, object=surface0
	ModifyGizmo setDisplayList=1, object=axes0
	ModifyGizmo autoscaling=1
	ModifyGizmo currentGroupObject=""
	ModifyGizmo showInfo
	ModifyGizmo infoWindow={551,23,1368,320}
	ModifyGizmo endRecMacro
	ModifyGizmo SETQUATERNION={0.531194,-0.220652,-0.320213,0.752734}
	ColorScale/C/N=text0/X=2.75/Y=20.45 surfaceFill=surface0
EndMacro
```

### *See Also* {#see-also}
For all other flags see [TextBox](/igorpro/commands/textbox.md) and [AppendText](/igorpro/commands/appendtext.md) operations.

[Color Scales](/igorpro/graphing/annotations.md#color-scales), [AnnotationInfo](/igorpro/commands/annotationinfo.md), [AnnotationList](/igorpro/commands/annotationlist.md)

### *Demo* {#demo}
[Open ColorScale Demo](#igor-pxp/Examples/Feature__Demos__2/ColorScale__Demo.pxp)