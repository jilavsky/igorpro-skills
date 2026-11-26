---
description: "The ModifyGraph operation modifies the target or named graph. This section of ModifyGraph relates to general graph window settings."
slug: /commands/modifygraph
---

<div className="command-signature">

## <strong>ModifyGraph</strong>  [/W=<em>winName</em> /Z] [<em>frameInset</em>= <em>i</em>, <em>frameStyle</em>= <em>f</em> , <em>gfMult</em>=<em>f</em>, <em>gFont</em>=<em>fontStr</em>, <em>gfSize</em>=<em>gfs</em>, <em>gfRelSize</em>=<em>pct</em>, <em>gmSize</em>=<em>gms</em>, <em>height</em>=<em>heightSpec</em>, <em>swapXY</em>=<em>s</em>, <em>useComma</em>=<em>uc</em>, <em>useDotForX</em>=<em>u</em>, <em>UIControl</em>=<em>f</em>, <em>useLongMinus</em>=<em>m</em>, <em>width</em>=<em>widthSpec</em>] {#modifygraph}

</div>

The ModifyGraph operation modifies the target or named graph. This section of ModifyGraph relates to ***general*** graph window settings. See also following sections:

[ModifyGraph for Traces](#modifygraph-for-traces)

[ModifyGraph for Axes](#modifygraph-for-axes)

[ModifyGraph for Colors](#modifygraph-for-colors)

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">expand = *e*</span> | Specifies the onscreen expansion (or magnification) factor of a graph. *e* may be zero or 0.125 to 8 times expansion. |
|  | Graph magnification affects only base graphs (not subwindowed graphs), and it affects only the onscreen display; it has **no** effect on graph exporting or printing. |
|  | When changing the magnification, the graph window will automatically resize itself except for negative values which are used in recreation macros where the size is already correct. |
| <span class="table-cell-nowrap">frameInset = *i*</span> | Specifies the number of pixels by which to inset the frame of the graph subwindow. |
| <span class="table-cell-nowrap">frameStyle = *f*</span> | specifies the frame style for a graph subwindow. Values for frameStyle are: |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>None</td></tr><tr><td>*f*&nbsp;=1:</td><td>Single</td></tr><tr><td>*f*&nbsp;=2:</td><td>Double</td></tr><tr><td>*f*&nbsp;=3:</td><td>Triple</td></tr><tr><td>*f*&nbsp;=4:</td><td>Shadow</td></tr><tr><td>*f*&nbsp;=5:</td><td>Indented</td></tr><tr><td>*f*&nbsp;=6:</td><td>Raised</td></tr><tr><td>*f*&nbsp;=7:</td><td>Text well</td></tr></tbody></table>
|  | The last three styles are fake 3D and will look good only if the background color of the enclosing space and the table itself is a light shade of gray. |
| <span class="table-cell-nowrap">gfMult = *f*</span> | Multiplies font and marker size by *f* percent. Clipped to between 25% and 400%; it is applied after all other font and marker size calculations. |
| <span class="table-cell-nowrap">gFont = *fontStr*</span> | Specifies the name of the default font for the graph, overriding the normal default font. The normal default font for a subgraph is obtained from its parent while a base graph uses the value set by the [DefaultFont](/igorpro/commands/defaultfont.md) operation. |
| <span class="table-cell-nowrap">gfSize = *gfs*</span> | Sets the default size for text in the graph. Normally, the default size for text is proportional to the graph size; gfSize will override that calculation as will the gfRelSize method. Use a value of -1 to make a subgraph get its default font size from its parent. |
| <span class="table-cell-nowrap">gfRelSize = *pct*</span> | Specifies the percentage of the graph size to use in calculating a default size for text in the graph. This overrides Igor's normal method for setting the default font size as a function of the graph size. When used, the default marker size is set to one third the font size. Use a value of 0 to revert to the default method. |
| <span class="table-cell-nowrap">gmSize = *gms*</span> | Sets the default size for markers in the graph. Use a value of -1 to make a subgraph get its default marker size from its parent. |
| <span class="table-cell-nowrap">height = *heightSpec*</span> | Sets the height for the graph area. See the examples. |
| swapXY=*s* |<table class="nested-table"><tbody><tr><td>*s*=0:</td><td>Normal orientation of X and Y coordinates.</td></tr><tr><td>*s*=1:</td><td>Swap X and Y values to plot Y coordinates versus the horizontal axes and X coordinates versus the vertical axes. The effect is similar to mirroring the graph about the lower-left to upper-right diagonal.</td></tr></tbody></table>
| useComma=*uc* |<table class="nested-table"><tbody><tr><td>*uc*&nbsp;=0:</td><td>Use period as decimal separator and comma as thousands separator (default).</td></tr><tr><td>*uc*&nbsp;=1:</td><td>Use comma as decimal separator and period as the thousands separator. This does not alter the presentation of numbers in \{*expression*} constructs in annotations.</td></tr></tbody></table>
| <span class="table-cell-nowrap">useDotForX = *u*</span> | In the display of axis labels, if *u* =1 then, in instances of exponential notation such as "5x10<sup>3</sup>", the normal "x" is replaced with a dot giving "5·10<sup>3</sup>". useDotForX was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">UIControl = *f*</span> | Disables certain aspects of the user interface for graphs. The UIControl keyword, added in Igor Pro 7.00, is for use by advanced Igor programmers who want to disable user actions. |
|  | This is a bitwise setting. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | *f* is defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Disable axis click. Prevents moving or otherwise modifying an axis.</td></tr><tr><td>Bit&nbsp;1:</td><td>Disable cursor click. Prevents moving a graph cursor.</td></tr><tr><td>Bit&nbsp;2:</td><td>Disable trace drag. Prohibits the click-and-hold action to offset a trace on the graph.</td></tr><tr><td>Bit&nbsp;3:</td><td>Disable marquee. When set, you can&#39;t make a marquee on the graph, which in turn prevents changing the range of the graph using the marquee.</td></tr><tr><td>Bit&nbsp;4:</td><td>Disable draw mode.</td></tr><tr><td>Bit&nbsp;5:</td><td>Disable double click. Prohibits any double-click action. In general, double-clicks in a graph bring up dialogs to modify the graph&#39;s appearance.</td></tr><tr><td>Bit&nbsp;6:</td><td>Disable clicks on annotations. Prevents modification of annotations.</td></tr><tr><td>Bit&nbsp;7:</td><td>Disable tooltips.</td></tr><tr><td>Bit&nbsp;8:</td><td>Disable contextual menus.</td></tr><tr><td>Bit&nbsp;9:</td><td>Disable marquee menu. With this set, you can still have a marquee and use it for, i.e., selecting some portion of the graph, but you can&#39;t use the maruqee menu to change the graph&#39;s range. Note that if bit 3 is set, this bit is moot.</td></tr><tr><td>Bit&nbsp;10:</td><td>Disable mouse wheel events. This will prevent axis scaling using the mouse wheel.</td></tr><tr><td>Bit&nbsp;11:</td><td>Disable option-drag. Prevents offsetting the graph by holding down the Alt key and then dragging in the plot area.</td></tr></tbody></table>
|  | To disable items in the Graph menu use [SetIgorMenuMode](/igorpro/commands/setigormenumode.md). |
| <span class="table-cell-nowrap">useLongMinus = *m*</span> | Uses a normal (*m* =0; default) or long dash (*m* =1) for the minus sign. |
| <span class="table-cell-nowrap">width = *widthSpec*</span> | Sets the width for the graph area. See the examples. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Modifies the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/Z</span> | Doesn't generate an error in style macros if the indexed trace, named wave, or named axis does not exist. |

### *Examples* {#examples}
Execute the following lines to create a graph where all the text expands and contracts directly in relation to the window size:


```igor
Make jack=sin(x/8);display jack
ModifyGraph mode=4,marker=8,gfRelSize= 5.0
TextBox/N=text0/A=MC "Some \\Zr200big\\]0 and \\Zr050small\\]0\rtext"
```

The *widthSpec* and *heightSpec* set the width and height mode for the top graph. The following examples illustrate how to specify the various modes.


```igor
ModifyGraph width=0, height=0           // set to auto height, width mode.
                                        // The width and height of horizontal
                                        // and vertical axes are automatically
                                        // determined by Igor based on the
                                        // overall size of the graph and other
                                        // factors such as axis offset setting
                                        // and the effect of exterior textboxes.
                                        // This is the normal, default mode.

Variable n=72*5	                        // five inches as points
ModifyGraph width=n                     // absolute width mode, horizontal axis 
                                        // width constrained to n points

ModifyGraph height=n                    // absolute height mode, n is in points
                                        // The height of the vertical axes is
                                        // constrained to n points.

Variable n=2
ModifyGraph width={perUnit,n,bottom}    // per unit width mode
                                        // The width of the horizontal
                                        // axes is n points times the
                                        // range of the bottom axis.

ModifyGraph height={Aspect,n}           // aspect height mode, n is aspect ratio
                                        // The height of the vertical axes is
                                        // n times width of the horizontal axes.

ModifyGraph width={Plan,n,bottom,left}  // plan width mode.
                                        // The width of the horizontal
                                        // axes is n times height of
                                        // vertical axes times range of
                                        // the bottom axis divided by
                                        // the range of the left axis.
```

### *See Also* {#see-also}
[ModifyGraph for Traces](#modifygraph-for-traces)

[ModifyGraph for Axes](#modifygraph-for-axes)

[ModifyGraph for Colors](#modifygraph-for-colors)


<!-- IndentedSubtopic -->
## ModifyGraph for Traces {#modifygraph-for-traces}

<div className="command-signature">

## <strong>ModifyGraph</strong>  [/W=<em>winName</em> /Z] <em>key</em> [(<em>traceName</em>)] = <em>value</em> [, <em>key</em> [(<em>traceName</em>)] = <em>value</em>]... {#modifygraph-for-traces}

</div>

This section of ModifyGraph relates to modifying the appearance of wave "traces" in a graph. A trace is a representation of the data in a wave, usually connected line segments.

### *Parameters* {#modifygraph-for-traces-parameters}
Each parameter has the syntax:

*key* [(*traceName*)] = *value*

Each *key* parameter may take an optional *traceName* enclosed in parentheses. Usually *traceName* is simply the name of a wave displayed in the graph, as in "mode(myWave)=4". If the "(*traceName*)" is omitted, all traces in the graph are affected. For instance, "ModifyGraph lSize=0.5" sets the lines size of all traces to 0.5 points.

More precisely, *traceName* is a wave name, optionally followed by the # character and an instance number. For example, "mode(myWave#1)=4".

A string containing a trace name can be used with the $ operator to specify *traceName*. For example, "String MyTrace="myWave#1"; mode($MyTrace)=4".

Though not shown in the syntax, the optional "(*traceName*)" may be replaced with "[*traceIndex*]", where *traceIndex* is zero or a positive integer denoting the trace to be modified. "[0]" denotes the first trace appended to the graph, "[1]" denotes the second trace, etc. This syntax is used for style macros, in conjunction with the /Z flag.

For certain modes and certain properties, you can set the conditions at a specific point on a trace by appending the point number in square brackets after the trace name. For more information, see the Customize at Point section below.

The parameter descriptions below omit the optional "(*traceName*)". When using ModifyGraph from a user-defined function, be careful not to pass wave references to ModifyGraph. ModifyGraph expects trace names, not wave references. See [Trace Name Parameters](/igorpro/programming/programming.md#trace-name-parameters) for details.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">arrowMarker = 0</span> |  |
| <span class="table-cell-nowrap">arrowMarker = {*aWave*,*lineThick*,*headLen*,*headFat*,*posMode* [,*barbSharp*=*b*,*barbSide*=*s*,*frameThick*=*f*]}</span> |  |
|  | Draws arrows instead of conventional markers at each data point in a wave. Arrows are not clipped to the plot area and will be drawn wherever a data point is within the plot area. |
|  | *aWave* contains arrow information for each data point. It is a two (or more) column wave containing arrow line lengths (in points) in column 0 and angles (in radians measured counterclockwise) in column 1. Zero angle is a horizontal arrow pointing to the right. If an arrow is below the minimum length of 4 points, a default marker is drawn. |
|  | Additional columns may be supplied in *aWave* to control parameters on a point by point basis. These optional columns are specified by dimension label and not by specific column numbers. The labels are *lineThick*, *headLen*, and *headFat* and correspond to the same parameters listed above. |
|  | You can change arrow markers into standard meteorological wind barbs by adding a column to *aWave* and giving it a column label of windBarb. Values are integers from 0 to 40 representing wind speeds up to 4 flags. Use positive integers for clockwise barbs and negative for the reverse. Use NaN to suppress the drawing. See [Wind Barb Plots](/igorpro/graphing/graphs.md#wind-barb-plots) for an example. |
|  | *lineThick* is the line thickness in Points. |
|  | *headLen* is the arrow head length in Points. |
|  | *headFat* controls the arrow fatness. It is the width of the arrow head divided by the length. |
|  | *posMode* specifies the arrow location relative to the data point. |
|  |<table class="nested-table"><tbody><tr><td>*posMode*&nbsp;=0:</td><td>Start at point.</td></tr><tr><td>*posMode*&nbsp;=1:</td><td>Middle on point.</td></tr><tr><td>*posMode*&nbsp;=2:</td><td>End at point.</td></tr></tbody></table>
|  | In addition to the wave specification, *aWave* can also be the literal "\_inline\_" to draw lines and arrows between points on the trace (see ***Examples*** below). If *aWave* is \_inline\_, *posMode* values are: |
|  |<table class="nested-table"><tbody><tr><td>*posMode*&nbsp;=0:</td><td>Arrow at start.</td></tr><tr><td>*posMode*&nbsp;=1:</td><td>Arrow in middle.</td></tr><tr><td>*posMode*&nbsp;=2:</td><td>Arrow at end.</td></tr><tr><td>*posMode*&nbsp;=3:</td><td>Arrow in middle pointing backwards.</td></tr></tbody></table>
|  | You can also enable inline mode even if *aWave* is not \_inline\_ by setting posMode to values between 4 and 7. These are the same as modes 0-3 above. |
|  | Optional parameters must be specified using *keyword* = *value* syntax and can only be appended after *posMode* in any order. |
|  | *barbSharp* is the continuously variable barb sharpness between -1.0 and 1. 0: |
|  |<table class="nested-table"><tbody><tr><td>*barbSharp*&nbsp;=&nbsp;1:</td><td>No barb; lines only.</td></tr><tr><td>*barbSharp*&nbsp;=&nbsp;0:</td><td>Blunt (default).</td></tr><tr><td>*barbSharp*&nbsp;=&nbsp;-1:</td><td>Diamond.</td></tr></tbody></table>
|  | *barbSide* specifies which side of the line has barbs relative to a right-facing arrow: |
|  |<table class="nested-table"><tbody><tr><td>*barbSide*&nbsp;=0:</td><td>None.</td></tr><tr><td>*barbSide*&nbsp;=1:</td><td>Top.</td></tr><tr><td>*barbSide*&nbsp;=2:</td><td>Bottom.</td></tr><tr><td>*barbSide*&nbsp;=3:</td><td>Both (default).</td></tr></tbody></table>
|  | *frameThick* specifies the stroke outline thickness of the arrow in points. The default is *frameThick* = 0 for solid fill. |
|  | *aWave* can contain columns with data for each optional parameter using matching column names. |
|  | [Open Barbs And Arrows Demo](#igor-pxp/Examples/Feature__Demos__2/Barbs__And__Arrows.pxp) |
| <span class="table-cell-nowrap">barStrokeRGB = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Specifies a separate color for bar strokes (outlines) if useBarStrokeRGB is 1. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
|  | Applies only to Histogram Bars drawing mode (mode=5). |
|  | The bar fill color continues to be set with the rgb=(*r,g,b*[,*a*]), zColor={...}, usePlusRGB, plusRGB=(*r*,*g*,*b*[,*a*]), useNegRGB, and negRGB=(*r*,*g*,*b*[,*a*]) parameters. |
|  | Use barStrokeRGB and useBarStrokeRGB to put a differently-colored outline around Histogram Bars: |
|  | <img src="Images/ModifyGraph/ModifyGraph_0.png" width="100%"/> |
| <span class="table-cell-nowrap">cmplxMode = *c*</span> | Display method for complex waves. |
|  |<table class="nested-table"><tbody><tr><td>*c*&nbsp;=0:</td><td>Default mode displays both real and imaginary parts (imaginary part offset by dx/2).</td></tr><tr><td>*c*&nbsp;=1:</td><td>Real part only.</td></tr><tr><td>*c*&nbsp;=2:</td><td>Imaginary part only.</td></tr><tr><td>*c*&nbsp;=3:</td><td>Magnitude.</td></tr><tr><td>*c*&nbsp;=4:</td><td>Phase (radians).</td></tr></tbody></table>
|  | *cmplxMode*=0 does not work when the trace is a subrange of a multidimensional wave. |
| <span class="table-cell-nowrap">column = *n*</span> | Changes the displayed column from a matrix. Out of bounds values are clipped. |
| gaps=*g* |<table class="nested-table"><tbody><tr><td>*g*&nbsp;=0:</td><td>No gaps (ignores NaNs).</td></tr><tr><td>*g*&nbsp;=1:</td><td>(default) Gaps (shows NaNs as gaps).</td></tr></tbody></table>
|  | Note: to display gaps for masked values, use the optional gap parameter to the mask command. |
| gradient | See [Gradient Fills](/igorpro/graphing/making-figures/graphics.md#gradient-fills) for parameters and details. |
| gradientExtra | See [Gradient Fills](/igorpro/graphing/making-figures/graphics.md#gradient-fills) for parameters and details. |
| <span class="table-cell-nowrap">hBarNegFill = *n*</span> | Fill kind for negative areas if useNegPat is true. *n* is the same as for the hbFill keyword. |
| <span class="table-cell-nowrap">hbFill = *n*</span> | Sets the fill pattern. |
|  |<table class="nested-table"><tbody><tr><td>*n*&nbsp;=0:</td><td>No fill</td></tr><tr><td>*n*&nbsp;=1:</td><td>Erase</td></tr><tr><td>*n*&nbsp;=2:</td><td>Solid black.</td></tr><tr><td>*n*&nbsp;=3:</td><td>75% gray</td></tr><tr><td>*n*&nbsp;=4:</td><td>50% gray</td></tr><tr><td>*n*&nbsp;=5:</td><td>25% gray.</td></tr><tr><td>*n*&nbsp;=&nbsp;6...77:</td><td>See [Fill Patterns](/igorpro/graphing/making-figures/graphics.md#fill-patterns).</td></tr></tbody></table>
| <span class="table-cell-nowrap">hideTrace = *h*</span> | Removes a trace from the graph display. |
|  |<table class="nested-table"><tbody><tr><td>*h*=0:</td><td>Shows the trace if it is hidden.</td></tr><tr><td>*h*=1:</td><td>Hides the trace and removes it from autoscale calculations.</td></tr><tr><td>*h*=2:</td><td>Hides the trace.</td></tr></tbody></table>
|  | When using *h*=1 to hide a graph trace, the hidden trace symbol and following text in annotations are also hidden. The amount of hidden text is the lesser of: 1) the remaining text on the same line or 2) the text up to but not including another trace symbol "\s(traceName)". |
| <span class="table-cell-nowrap">lHair = *lh*</span> | Sets the hairline factor for a trace printed on a PostScript® printer. |
| <span class="table-cell-nowrap">lineJoin = {*j, ml*}</span> | Sets the line join style and miter limit. |
|  | Line join: |
|  |<table class="nested-table"><tbody><tr><td>*j*&nbsp;=0:</td><td>Miter joins</td></tr><tr><td>*j*&nbsp;=1:</td><td>Round joins</td></tr><tr><td>*j*&nbsp;=2:</td><td>Bevel joins (default)</td></tr></tbody></table>
|  | Miter limit: |
|  |<table class="nested-table"><tbody><tr><td>*ml*&nbsp;&gt;=&nbsp;1:</td><td>Sets miter limit to *ml*</td></tr><tr><td>*ml*&nbsp;=&nbsp;INF:</td><td>Sets miter limit to unlimited</td></tr><tr><td>*ml*&nbsp;=&nbsp;0:</td><td>Leaves miter limit unchanged</td></tr><tr><td>*ml*&nbsp;=&nbsp;-1:</td><td>Sets miter limit to default (10)</td></tr></tbody></table>
|  | The miter limit applies only to miter joins (*j* =0) and is ignored otherwise. |
|  | See [Line Join and End Cap Styles](/igorpro/graphing/making-figures/graphics.md#line-join-and-end-cap-styles) for further information. |
|  | The lineJoin keyword was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">live = *lv*</span> | *lv* is a bitwise parameter defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Live mode (see Live Mode below)</td></tr><tr><td>Bit&nbsp;1:</td><td>Fast line drawing (see Fast Line Drawing below)</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">lSize = *l*</span> | Sets the line thickness, which can be fractional or zero, which hides the line. |
| logZColor=*lzc* |<table class="nested-table"><tbody><tr><td>*lzc*&nbsp;=0:</td><td>Sets the default linearly-spaced zColors (see the zColor parameter).</td></tr><tr><td>*lzc*&nbsp;=1:</td><td>Turns on logarithmically-spaced zColors. This requires that the *zWave* values be greater than 0 to display correctly.</td></tr></tbody></table>
|  | Affects trace line color only when the zColor parameter is used with a color table or color index wave - it has no effect if rgb=(*r*,*g*,*b*) parameter or zColor={...,directRGB} are used. |
| <span class="table-cell-nowrap">lOptions = *cap*</span> | Sets the line end cap style: |
|  |<table class="nested-table"><tbody><tr><td>*cap*=0:</td><td>Flat caps</td></tr><tr><td>*cap*=1:</td><td>Round caps</td></tr><tr><td>*cap*=2:</td><td>Square caps (default)</td></tr></tbody></table>
|  | See [Line Join and End Cap Styles](/igorpro/graphing/making-figures/graphics.md#line-join-and-end-cap-styles) for further information. |
| <span class="table-cell-nowrap">lSmooth = *ls*</span> | Sets the smoothing factor for a trace printed on a PostScript® printer. |
| <span class="table-cell-nowrap">lStyle = *s*</span> | Sets trace line style or dash pattern. |
|  |<table class="nested-table"><tbody><tr><td>*s*&nbsp;=0:</td><td>Solid lines.</td></tr><tr><td>*s*&nbsp;=1...17:</td><td>Specified dashed line style.</td></tr></tbody></table>
|  | <img src="Images/ModifyGraph/ModifyGraph_1.png" width="70%"/> |
| <span class="table-cell-nowrap">marker = *n*</span> | *n* =0 to 62 designates various markers if mode=3 or 4. |
|  | You can also create custom markers. See [Custom Marker Hook Functions](/igorpro/advanced-topics.md#custom-marker-hook-functions). |
|  | If a marker can't be drawn, for example because *n* is not a valid marker number or a custom marker's hook function is missing or does not draw the marker, Igor draws a ? in its place. |
|  | See [Markers](/igorpro/graphing/graphs.md#markers) for a table of marker values. |
| <span class="table-cell-nowrap">mask = {*maskwave*,*mode*,*value [, gap]*} or 0</span> |  |
|  | Specifies individual points for display by comparing values in *maskWave* with *value* as specified by *mode*. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Exclude if equal.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Include if equal.</td></tr><tr><td>*mode*&nbsp;=2:</td><td>Include if bitwise AND is true.</td></tr><tr><td>*mode*&nbsp;=3:</td><td>Include if bitwise AND is false.</td></tr></tbody></table>
|  | *maskwave* can be specified using subrange notation. The length of *maskwave* (or subrange) must match the size of specified trace's wave (or subrange.) Bitwise modes should be used with integer waves with the intent of using one mask wave with multiple traces. (See Examples below.) |
| The optional gap value was added in Igor 10; it defaults to 0 which maintains the behavior of drawing over masked value(s) and connecting the non-masked values. Normally this means a line is drawn between the non-masked values. |  |
|  | Setting gap to 1 leaves gaps where the masked values are. The gap setting is independent of ModifyGraph gap (which applies to NaN values, not to masked values). |
| <span class="table-cell-nowrap">mode = *m*</span> | Sets trace display mode. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Lines between points.</td></tr><tr><td>*m*&nbsp;=1:</td><td>Sticks to zero.</td></tr><tr><td>*m*&nbsp;=2:</td><td>Dots at points.</td></tr><tr><td>*m*&nbsp;=3:</td><td>Markers.</td></tr><tr><td>*m*&nbsp;=4:</td><td>Lines and markers.</td></tr><tr><td>*m*&nbsp;=5:</td><td>Histogram bars.</td></tr><tr><td>*m*&nbsp;=6:</td><td>Cityscape.</td></tr><tr><td>*m*&nbsp;=7:</td><td>Fill to zero.</td></tr><tr><td>*m*&nbsp;=8:</td><td>Sticks and markers.</td></tr></tbody></table>
| <span class="table-cell-nowrap">mrkFillRGB = (*r*,*g*,*b*[,*a*])</span> | Sets the background fill color for hollow markers. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
|  | This setting takes effect only if opaque is set to non-zero. See opaque keyword below. |
|  | The mrkFillRGB keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">mrkStrokeRGB = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Specifies the color for marker stroked lines if useMrkStrokeRGB is 1. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
|  | The marker fill color continues to be set with the rgb=(*r,g,b*[,*a*]) or zColor={...} parameters. |
|  | Applies only to the nontext and nonarrow marker modes. |
|  | Use mrkStrokeRGB and useMrkStrokeRGB to put a colored outline around filled markers, such as marker=19: |
|  | <img src="Images/ModifyGraph/ModifyGraph_2.png" width="100%"/> |
|  | <div><Admonition type="note"><p>The stroke color of unfilled markers such as marker 8 is also affected by mrkStrokeRGB, but their fill color is only affected by the opaque parameter (and the opaque fill color is always white, so if you want a color-filled marker, don't use unfilled markers).</p></Admonition></div> |
| <span class="table-cell-nowrap">mrkThick = *t*</span> | Sets the thickness of markers in points (can be fractional). |
| <span class="table-cell-nowrap">msize = *m*</span> | Specifies the marker size in points. |
|  | *m* =0 means autosize markers. |
|  | *m* greater than zero sets marker size. |
|  | *m* can be fractional. This will only make a difference when the graph is printed because fractional points cannot be displayed on the screen. |
| <span class="table-cell-nowrap">mskip = *n*</span> | Puts a marker on only every *n*th data point in lines and markers mode (mode=4). Useful for displaying many data points when you want to identify the traces with markers. The maximum value for *n* is 32767. |
| <span class="table-cell-nowrap">mstandoff = *s*</span> | Prevents lines from touching markers in lines and markers mode if s is greater than zero. *s* is in units of points. This feature was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">muloffset = {*mx*,*my*}</span> | Sets the display multiplier for X (*mx*) and Y (*my*). The effective value for a given X or Y data point then becomes *muloffset* **data* +*offset*. A value of zero means "no multiplier" -- not multiply by zero. |
| <span class="table-cell-nowrap">negRGB = (*r*,*g*,*b*[,*a*])</span> | Specifies the color for negative values represented by the trace if useNegRGB is 1. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">offset = {*x*,*y*}</span> | Sets the display offset in horizontal (*x*) and vertical (*y*) axis units. |
| <span class="table-cell-nowrap">opaque = *o*</span> | Displays transparent (*o* =0) or opaque (*o* =1) markers. |
|  | If *o* is zero (default) hollow markers such as unfilled circles and boxes have transparent backgrounds. If *o* is non-zero, the background is filled with color. The color defaults to white, but you can change it using the mrkFillRGB keyword. |
| <span class="table-cell-nowrap">patBkgColor = 0, 1, 2 or (r,g,b[,*a*])</span> |  |
|  | Specifies the background color for fill patterns. |
|  | 0, the default, is white, 1 is graph background, 2 is transparent. |
|  | Use (r,g,b[,*a*]) for a specific RGB color. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">plotClip = *p*</span> | *p* =1 clips the trace by the operating system (not by Igor) to the plot rectangle. This trims overhanging markers and thick lines. On Windows, this may not be supported on certain printers or by certain applications when importing. |
| <span class="table-cell-nowrap">plusRGB = (*r*,*g*,*b*[,*a*])</span> | Specifies the color for positive values represented by the trace if usePlusRGB is 1. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">quickdrag = *q*</span> | *q*=0 for normal traces. |
|  | *q*=1 for traces that can be instantly dragged without the normal one second delay. See the Quickdrag section below. |
|  | *q*=2 causes the mouse cursor to change to 4 arrows when over the trace and a reduced search is used. |
| <span class="table-cell-nowrap">removeCustom = *r*</span> | Removes per-point trace customizations. See [Customize at Point](/igorpro/graphing/graphs.md#customize-at-point) for background information. The removeCustom keyword was added in Igor Pro 9.00. |
|  | The parameter *r* is required by the ModifyGraph syntax, but its value is immaterial. We recommend using 1 for *r* but any number will work. |
|  | These examples show how to use the removeCustom keyword given a graph with a trace named wave0: |
|  | <code class="igor">// Remove customizations for point 3 of trace wave0&#10;ModifyGraph removeCustom(wave0[3]) = 1&#10;&#10;// Remove customizations for all points of trace wave0&#10;ModifyGraph removeCustom(wave0) = 1&#10;&#10;// Remove customizations for all points of all traces&#10;ModifyGraph removeCustom = 1</code> |
| <span class="table-cell-nowrap">rgb = (*r*,*g*,*b*[,*a*])</span> | Specifies the color of the trace. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">textMarker = {<*char or wave* >,*font*,*style*,*rot*,*just*,*xOffset*,*yOffset*} or 0</span> |  |
|  | Uses the specified character or text from the specified wave in place of the marker for each point in the trace. |
|  | If the first parameter is a quoted string or a string expression of the form "" + *strexpr* in a user function, ModifyGraph uses the first three bytes of the string as the marker for all points. Three bytes are supported mainly for non-ASCII characters but can be used for 3 separate single-byte characters. Otherwise, it interprets the first parameter as the name of a wave. If the wave is a text wave, it uses the value of each point in the text wave as the marker for the corresponding point in the trace. If the wave is a numeric wave, the value for each point is converted into text and the result is used as the marker for the corresponding point in the trace. |
|  | *xOffset* and *yOffset* are offsets in fractional points. Each marker will be drawn offset from the location of the corresponding point in the trace by these amounts. |
|  | *style* is a font style code as used with the ModifyGraph fstyle keyword. |
|  | *rot* is a text rotation between -360 and 360 degrees. |
|  | *just* is a justification code as used in the [DrawText](/igorpro/commands/drawtext.md) operation except the x and y codes are combined as y*4+x. Use 5 for centered. |
|  | The font size is 3*marker size. Note that marker size and color can be dynamically set via the zColor and zmrkSize keywords. |
| <span class="table-cell-nowrap">toMode = *t*</span> | toMode modifies the behavior of the display modes as determined by the mode parameter. |
|  |<table class="nested-table"><tbody><tr><td>*t*&nbsp;=0:</td><td>Fill-to-zero.</td></tr><tr><td>*t*&nbsp;=1:</td><td>Fill to next trace. Applies to sticks to zero (mode=1), histogram bars (mode=5) and fill-to-zero (mode=7).</td></tr><tr><td>*t*&nbsp;=2:</td><td>Means add the current trace&#39;s Y values to the next trace&#39;s Y values. Works with all display modes.</td></tr><tr><td>*t*&nbsp;=3:</td><td>Means stack on next and is the same as *t* =2 except that the added value is clipped to zero. Works with all display modes.</td></tr><tr><td>*t*&nbsp;=-1:</td><td>This mode is used only with category plots and means &quot;keep with next&quot; (i.e., put in the same subcategory as the next trace). It is used for special effects only.</td></tr></tbody></table>
|  | For modes 1, 2 and 3, both Y-waves must have the same number of points and must use the same X values. Igor uses the X values from the first wave for both Y-waves. |
| <span class="table-cell-nowrap">traceName = *name*</span> | Sets, changes, or removes a custom trace name. |
|  | The traceName keyword was added in Igor Pro 9.00. |
|  | By default Igor assigns trace names based on the name of the displayed wave. You can assign a custom trace name when appending a wave to a graph using the /TN flag with the [Display](/igorpro/commands/display.md) and [AppendToGraph](/igorpro/commands/appendtograph.md) operations. See [Trace Names](/igorpro/graphing/graphs.md#trace-names) for details. |
|  | The traceName keyword allows you to change the name of a trace after it has been added to a graph. For example: |
|  | <code class="igor">Make/O wave0&#10;Display wave0&#10;ModifyGraph traceName(wave0)=Custom0</code> |
|  | Use $"" for *name* to remove the custom name and revert to the default trace name: |
|  | <code class="igor">ModifyGraph traceName(Custom0)=$""</code> |
|  | Renaming a trace can change the names of other traces in the graph from the same wave. For example, if you display two instances of wave0 in one graph, the first trace name is wave0 and the second is wave0#1. If you now rename trace wave0, the name of the second instance of wave0 changes from wave0#1 to wave0. See [Instance Notation](/igorpro/programming/commands.md#instance-notation) for further discussion. |
| <span class="table-cell-nowrap">useBarStrokeRGB = *u*</span> | If *u* =1 then bar stroked lines use the color specified by the barStrokeRGB keyword. |
|  | Applies only to Histogram Bars drawing mode (mode=5). |
|  | The bar fill color continues to be set by the rgb, zColor, usePlusRGB, plusRGB, useNegRGB, and negRGB keywords. |
|  | if *u* =0 then the bar stroked line colors are set with the rgb=(*r,g,b*[,*a*]) or zColor={...} parameters, just like the bar fill color. |
| <span class="table-cell-nowrap">useMrkStrokeRGB = *u*</span> | If *u* =1 then marker stroked lines use the color specified by the mrkStrokeRGB keyword. The marker fill color continues to be set with the rgb=(*r,g,b*[,*a*]) or zColor={...} parameters. |
|  | Applies only to the nontext and nonarrow marker modes. |
|  | if *u*=0 then the marker stroked line colors are set with the rgb=(*r,g,b*[,*a*]) or zColor={...} parameters, just like the marker fill color. |
| <span class="table-cell-nowrap">useNegPat = *u*</span> | If *u* =1 then negative fills use the mode specified by the hBarNegFill keyword. Applies to the fill-to-zero,  fill-to-next and histogram bar modes. |
| <span class="table-cell-nowrap">useNegRGB = *u*</span> | If *u* =1 then negative fills use the color specified by the negRGB keyword. Applies to the fill-to-zero,  fill-to-next and histogram bar modes. |
| <span class="table-cell-nowrap">usePlusRGB = *u*</span> | If *u* =1 then positive fills use the color specified by the plusRGB keyword. Applies to the fill-to-zero,  fill-to-next and histogram bar modes. |
| <span class="table-cell-nowrap">userData = {*udName*, *doAppend*, *data*}</span> |  |
|  | Attaches arbitrary data to a trace. You should specify a trace name (userData(\<traceName\>)={...}). Otherwise copies of the data will be attached to *every* trace, which is most likely *not* what you intend. |
|  | Use the [GetUserData](/igorpro/commands/getuserdata.md) function to retrieve the data, with the trace name as the object ID. |
|  |<table class="nested-table"><tbody><tr><td>*udName*:</td><td>The name of your user data. Use The name of your user data. Use $&quot;&quot; for unnamed user data.</td></tr><tr><td>*doAppend*=0:</td><td>Do not append. Any pre-existing data is replaced.</td></tr><tr><td>*doAppend*=1:</td><td>Append the data. Data is added to the end of any pre-existing data.</td></tr><tr><td>*data*:</td><td>A string expression containing the data you wish to attach to the trace.</td></tr></tbody></table>
| <span class="table-cell-nowrap">zColor = {*zWave,zMin,zMax,ctName* [,*reverseMode* [,*cWave* ] ]} or 0</span> |  |
|  | Dynamically sets color based on the values in *zWave* and color table name or mode specified by *ctName* . |
|  | *zWave* may be a subrange expression such as myZWave[2,9] when *zWave* has more points than the trace, in which case myZWave[2] provides the z value for the first point of the trace, and autoscaled *zMin* or *zMax* is determined over only the *zWave* subrange. |
|  | If a value in the *zWave* is NaN then a gap or missing marker will be observed. If a value is out of range it will be replaced with the nearest valid value. See also the zColorMax and zColorMin keywords. |
|  | *ctName* can be the name of a built-in color table as returned by the [CTabList](/igorpro/commands/ctablist.md) function, such as Grays or Rainbow, for color table mode, ctableRGB for color table wave mode, cindexRGB for color index wave mode, or directRGB for direct color wave mode. |
|  | ***zColor for Built-in Color Table Mode*** |
|  | This mode uses the values in *zWave* to select a color from a built-in color table. See [Color Tables](/igorpro/graphing/contour-plots.md#color-tables) for details. |
|  | *zWave* contains values that are used to select a color from the built-in color table specified by *ctName* . |
|  | *zMin* is the *zWave* value that maps to the first entry in the color table. Use * for *zMin* to autoscale it to the smallest value in *zWave*. |
|  | *zMax* is the *zWave* value that maps to the last entry in the color table. Use * for *zMax* to autoscale it to the largest value in *zWave*. |
|  | *ctName* is a built-in color table name such as Grays or Rainbow. See the [CTabList](/igorpro/commands/ctablist.md) function for a list of built-in color tables. |
|  | Set the *reverseMode* to 1 to reverse the color table lookup or to 0 use the normal lookup. If you omit *reverseMode* or specify -1, the reverse mode is unchanged. |
|  | *cWave* must be omitted. |
|  | Normally the colors from the color table are linearly distributed between *zMin* and *zMax*. Use `logZColor=1` to distribute them logarithmically. |
|  | Example zColor command using built-in color table: |
|  | <code class="igor">ModifyGraph zColor(data)={zWave,*,*,Rainbow}</code> |
|  | ***zColor for Color Table Wave Mode*** |
|  | This mode is like Built-in Color Table except that the colors are stored in a color table wave that you have created. A color table wave can be a 3 column RGB wave or a 4 column RGBA wave. See [Color Table Waves](/igorpro/graphing/image-plots.md#color-table-waves) for details. |
|  | *zWave* contains values that are used to select a color from the color table wave specified by *cWave*. |
|  | *zMin* is the *zWave* value that maps to the first entry in the color table wave. Use \* for *zMin* to autoscale it to the smallest value in *zWave*. |
|  | *zMax* is the *zWave* value that maps to the last entry in the color table wave. Use \* for *zMax* to autoscale it to the largest value in *zWave*. |
|  | *ctName* is ctableRGB. |
|  | Set the *reverseMode* to 1 to reverse the color table lookup or to 0 use the normal lookup. If you omit *reverseMode* or specify -1, the reverse mode is unchanged. |
|  | *cWave* is a reference to your color table wave. |
|  | Normally the colors from the color table are linearly distributed between *zMin* and *zMax*. Use *logZColor*=1 to distribute them logarithmically. |
|  | <code class="igor">// Example ctableRGB zColor command&#10;ColorTab2Wave Rainbow    // Creates M_Colors wave&#10;Rename M_Colors, MyColorTableWave&#10;ModifyGraph zColor(data)={zWave,*,*,ctableRGB,0,MyColorTableWave}</code> |
|  | ***zColor for Color Index Wave Mode*** |
|  | This mode is like Color Table Wave except that the values in *zWave* represent X indices in terms of *cWave* . You must create the RGB or RGBA color index wave and set its X scaling appropriately. See [Color Index Wave](/igorpro/graphing/contour-plots.md#color-index-wave) for details. |
|  | *zWave* contains values that are used to select a color from the color index wave specified by *cWave* . |
|  | *zMin* and *zMax* are not used and should be set to *. |
|  | *ctName* is cindexRGB. |
|  | Set the *reverseMode* to 1 to reverse the color table lookup or to 0 use the normal lookup. If you omit *reverseMode* or specify -1, the reverse mode is unchanged. Normally the *zWave* values select the color from the row of *cWave* whose X value is closest to the *zWave* value. *ReverseMode* =1 reverses the colors. |
|  | *cWave* is a reference to your color index wave. |
|  | Normally the colors from the color index wave are linearly distributed between the minimum and maximum X values of the color index wave. Use logZColor=1 to distribute them logarithmically. |
|  | <code class="igor">// Example cindexRGB zColor command:&#10;zColor(data)={myZWave,\*,\*,cindexRGB,0,M_colors}&#10;// M_colors is generated by ColorTab2Wave</code> |
|  | ***zColor for Direct Color Wave Mode*** |
|  | In direct color mode, *zWave* is an RGB or RGBA wave that directly specifies the color for each point in the trace. If *zWave* is 8-bit unsigned integer, then its color component values range from 0 to 255. For other numeric types, color component values range from 0 to 65535. See [ColorTab2Wave](/igorpro/commands/colortab2wave.md), which generates RGB waves, and [Direct Color Details](/igorpro/graphing/image-plots.md#direct-color-details). |
|  | *zWave* is an RGB or RGBA wave that directly specifies the color for each point of the trace. |
|  | *zMin* and *zMax* are not used and should be set to \*. |
|  | *ctName* is directRGB. |
|  | *reverseMode* is not applicable and should be omitted or set to 0. |
|  | *cWave* must be omitted. |
|  | <code class="igor">// Example directRGB zColor command&#10;zColor(data)={zWaveRGB,\*,\*,directRGB}</code> |
|  | ***Turning zColor Off*** |
|  | zColor = 0 turns the zColor modes off. |
| <span class="table-cell-nowrap">zColorMax = (*red*, *green*, *blue*)</span> |  |
|  | Sets the color of the trace for zColor={*zWave*,...} values greater than the zColor's *zMax.* Also turns zColorMax mode on. |
|  | The *red*, *green* and *blue* color values are in the range of 0 to 65535. |
| <span class="table-cell-nowrap">zColorMax = 1, 0, *or* NaN</span> |  |
|  | Turns zColorMax mode off, on, or transparent. These modes affect the color of zColor={*zWave*,...} values greater than the zColor's *zMax*. |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Turns zColorMax mode on. The color of the affected trace pixels is black or the last color set by zColorMax=(*red*, *green*, *blue*).</td></tr><tr><td>0:</td><td>Default; turns zColorMax mode off. The color of the affected trace pixels is the last color in the zColor&#39;s *ctname* color table.</td></tr><tr><td>NaN:</td><td>Transparent zColorMax mode. Affected trace pixels are not drawn.</td></tr></tbody></table>
| <span class="table-cell-nowrap">zColorMin = (*red*, *green*, *blue*)</span> |  |
|  | Sets the color of the trace for zColor={*zWave*,...} values less than the zColor's *zMin*. Also turns zColorMin mode on. |
|  | The *red*, *green* and *blue* color values are in the range of 0 to 65535. |
| <span class="table-cell-nowrap">zColorMin = 1, 0, *or* NaN</span> |  |
|  | Turns zColorMin mode off, on, or transparent. These modes affect the color of zColor={*zWave*,...} values less than the zColor's *zMin*. |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Turns zColorMin mode on. The color of the affected image pixels is black or the last color set by zColorMin=(*red*, *green*, *blue*).</td></tr><tr><td>0:</td><td>Default; turns zColorMin mode off. The color of the affected trace pixels is the first color in the zColor&#39;s *ctname* color table.</td></tr><tr><td>NaN:</td><td>Transparent zColorMin mode. Affected trace pixels are not drawn.</td></tr></tbody></table>
| <span class="table-cell-nowrap">zmrkNum = {*zWave*} or 0</span> |  |
|  | Dynamically sets the marker number for each point to the corresponding value in *zWave* . The values in *zWave* are the marker numbers (as used with the marker keyword). If a value in the *zWave* is NaN then no marker will be drawn for the corresponding point. If a value is out of range it will be replaced with the nearest valid value. |
|  | zmrkNum=0 turns this mode off. |
| <span class="table-cell-nowrap">zmrkSize = {*zWave,zMin,zMax,mrkMin,mrkMax,* [*axis*] } or 0</span> |  |
|  | Dynamically sets marker size based on values in *zWave*. See [Marker Size as f(z)](/igorpro/graphing/graphs.md#marker-size-as-f-z) for background information. |
|  | zmrkSize = 0 turns this mode off. |
|  | Use \* or a missing parameter for *zMin* and *zMax* to autoscale. *mrkMin* and *mrkMax* can be fractional. |
|  | *mrkMin* is the marker size to use when z equals *zMin* and *mrkMax* is the marker size to use when z equals *zMax*. *mrkMin* and *mrkMax* are not limits; they just set the linear relationship between z and marker size. |
|  | If a value in the *zWave* is NaN then the corresponding marker is not drawn. |
|  | The marker size is clipped to 400 on the high end and to 1 point on the low end. |
|  | *axis* is an optional parameter specifying an existing axis on the graph. It is supported in Igor Pro 9.00 and later. Passing $"" for *axis* is the same as omitting it. |
|  | If *axis* is specified, the values in *zWave* are interpreted as in units of the specified axis and specify the half-width of the marker to be drawn. For a circle marker, this is the radius of the marker. |
|  | If *axis* is specified, the *zMin*, *zMax*, *mrkMin*, and *mrkMax* parameters have no impact on the marker size unless you remove the specified axis in which case those parameters control the trace's marker sizes. |
|  | See [Marker Size as f(z) in Axis Units](/igorpro/graphing/graphs.md#marker-size-as-f-z-in-axis-units) for further information. |
| <span class="table-cell-nowrap">zpatNum = {*zWave*} or 0</span> |  |
|  | Dynamically sets the positive fill type/pattern number for each point to the corresponding value in *zWave* . The values in *zWave* are the pattern numbers (as used with the hbFill keyword). If a value in the *zWave* is NaN then the corresponding point will not be drawn. If a value is out of range it will be replaced with the nearest valid value. |
|  | zpatNum=0 turns this mode off. |

### *Flags* {#modifygraph-for-traces-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Modifies the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the Command Line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/Z</span> | Used for style macros. Doesn't generate an error if the indexed trace, named wave, or named axis does not exist. |

### *Details* {#details}
Waves supplied with zmrkSize, zmrkNum, and zColor may use [Subrange Display Syntax](/igorpro/graphing/graphs.md#subrange-display-syntax).

### *Live Mode* {#live-mode}
Bit 0 of live=*lv* controls live mode. Live mode improves graph update performance when one or more of the waves displayed in the graph is frequently modified, for example, if the waves are being acquired from a data acquisition system. Live mode traces do not autoscale axes.

### *Fast Line Drawing* {#fast-line-drawing}
Bit 1 of live=lv controls fast line drawing. When enabled, Igor draws traces in lines-between-points mode using custom fast code instead of the normal system drawing code. The result is not as esthetically pleasing but can be much faster and may be critical in data acquisition applications. The custom code is used only for drawing to the screen, not for exporting graphics.


|  |
| --- |
| Fast line drawing was added in Igor Pro 8.00. |

See also [Graphs and High-Resolution Displays](/igorpro/graphing/making-figures/graphics.md#graphs-and-high-resolution-displays).

### *Quickdrag* {#quickdrag}
Quick drag mode (quickdrag=1) is a special purpose mode for creating cross hair cursors using a package of Igor procedures. Normally you would have to click and hold on a trace for one second before entering drag mode. When quickdrag is in effect, there is no delay. If a trace is in quickdrag mode it should also be set to live mode. With this combination you can click on a trace and immediately drag it to a new XY offset. In addition to quick drag mode, the cross hair package relies on Igor to store information about the drag in a string variable if certain conditions are in effect. The string variable name (that you have to create) is S_TraceOffsetInfo. It must reside in a data folder that has the same name as the graph (not title!!) which in turn must reside in root:WinGlobals:. If these conditions are met, then after a trace is dragged, information will be stored in the string using the following key-value format: 

```
GRAPH:<name of graph>;XOFFSET:<x offset value>;YOFFSET:<y offset value>;TNAME:<trace name>;
```

### *Customize at Point* {#customize-at-point}
You can customize the appearance of individual points on a trace in a graph for bar, marker, dot and lines to zero modes using key(tracename[pnt])=value syntax. The point number must be a literal number and the trace name is required.

To remove a customization, use `key(tracename[-pnt-1])=value` where value is not important but must match the syntax for the keyword. The offset of -1 is needed because point numbers start from zero. You can also remove customizations using the removeCustom keyword described above.

Although the syntax is allowed for all trace modifiers, it has meaning only for the following: rgb, marker, msize, mrkThick, opaque, mrkFillRGB, mrkStrokeRGB, mstandoff, barStrokeRGB, hbFill, patBkgColor and lSize.

Note that useBarStrokeRGB and useMrkStrokeRGB are not needed. The act of using barStrokeRGB or mrkStrokeRGB is enough to customize the point. But as a convenience, since these are generated by the modify graph dialog, they are ignored if used with [pnt] syntax.

Also note that legend symbols can use [pnt] syntax like so:


```
\s(<tracename>[pnt])
```

Automatically generated legends automatically include symbols for customized points.

For example:


```igor
Make/O/N=10 jack=sin(x); Display jack
ModifyGraph mode=5,hbFill=6,rgb=(0,0,0)
ModifyGraph hbFill(jack[2])=7,rgb(jack[2])=(0,65535,0)
ModifyGraph rgb(jack[3])=(65535,0,0)
Legend/C/N=text1/F=0/A=MC
```

### *Examples* {#modifygraph-for-traces-examples}
Arrow markers:


```igor
Make/O/N=10 wave1= x; Display wave1
Make/N=(10,2) awave
awave[][0]= p*5             // length
awave[][1]= pi*p/9          // angle
ModifyGraph mode=3,arrowMarker(wave1)={awave,1,10,0.3,0}

// Now add an optional column to control headLen
Redimension/N=(-1,3) awave
awave[][2]= 7+p             // will be head length

// Note at this point there has been no change until the following is executed
SetDimLabel 1,2,headLen,awave
```

Creating meteorological wind barb symbols:


```igor
Make/O/N=50 jack= floor(x/10),jackx= mod(x,10)
Display jack vs jackx
Make/O/N=(50,3) jackbarb
jackbarb[][0]= 40               // length of stem
jackbarb[][1]= 45*pi/180        // angle (45deg)
jackbarb[][2]= p                // wind speed code
SetDimLabel 1,2,windBarb,jackbarb
ModifyGraph mode=3,arrowMarker(jack)={jackbarb,1,10,0.5,0}
ModifyGraph margin(top)=62,margin(right)=84
```

See also [Wind Barb Plots](/igorpro/graphing/graphs.md#wind-barb-plots) for another example.

Inline arrows and barb sharpness:

```igor
Make/O/N=20 wavex=cos(x/3),wavey=sin(x)
Display wavey vs wavex
ModifyGraph mode=3,arrowMarker={\_inline\_,1,20,.5,0,barbSharp= 0.2}
```

Use direct color mode to individually color each point in a trace:

```igor
Make jack=sin(x/8)
Make/N=(128,3)/B/U jackrgb
Display jack
ModifyGraph mode=3,marker=19
jackrgb= enoise(128)+128
ModifyGraph zColor(jack)={jackrgb,*,*,directRGB}
```

Masking Example #1: Exclude alternating values


```igor
Make/O/N=100 jack= (p&1) ? sin(x/8) : cos(x/8)          // odd points are sin, even points are cosine
Display jack
ModifyGraph mode(jack)=4, marker(jack)=19, gaps(jack)=0 // no gaps or mask or mask with gaps

Make/O/N=100 mjack= (p&1) ? 0 : 1   // create a mask that shows (0) odd points and hides (1) even points
ModifyGraph mask(jack)={mjack,0,1}  // hides (excludes) jack point if mjack mask value is 1

// now switch which points are masked (hidden)
mjack= (p&1) ? 1 : 0	// shows (0) even point and hides (1) odd points
```

Masking Example #2: Exclude subrange of data two ways: without and with a gap


```igor
// Create a rising edge with simulated noise spikes
Make/O/N=50 jill= 10*(1-exp(-x*x/200)) + gnoise(2)*(p>=32 && p<=36)
Display jill

// simulate missing data 
jill[15] = NaN

// normal display of data, no masking		   
ModifyGraph mode(jill)=4, marker=8, gaps(jill)=1    // gaps where the jill values are NaN (this is the default gaps settings)

// Make a mask that hides the noisy data
Duplicate/O jill, maskJill                          // mask is best the same length as what it masks
Make/O maskJill = (p>=32 && p<=36)                  // maskJill is 0 for "good" data, 1 for "noise" data

// Skip over the noisy data without any gap (no gap setting in mask keyword's parameters, which defaults it to 0)
ModifyGraph mask(jill)={maskJill,0,1}               // Exclude (skip) jill point if maskJill mask value is 1

// Instead of skipping the noisy data, show a gap where the noisy data is masked away
ModifyGraph mask(jill)={maskJill,0,1,1}             // add the optional gap parameter to the mask keyword parameters
```

### *See Also* {#modifygraph-for-traces-see-also}
[ModifyGraph](/igorpro/commands/modifygraph.md) (General settings)

[ModifyGraph for Axes](#modifygraph-for-axes)

[ModifyGraph for Colors](#modifygraph-for-colors)

[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)

### *Demos* {#demos}
[Open Colors, Markers, Lines, Patterns Demo](#igor-pxp/Examples/Feature__Demos__2/ColorsMarkersLinesPatterns.pxp)

[Open Arrow Plot Demo](#igor-pxp/Examples/Graphing__Techniques/Arrow__Plot.pxp)


<!-- IndentedSubtopic -->
## ModifyGraph for Axes {#modifygraph-for-axes}

<div className="command-signature">

## <strong>ModifyGraph</strong>  [/W=<em>winName</em> /Z] <em>key</em> [(<em>axisName</em>)] = <em>value</em> [, <em>key</em> [(<em>axisName</em>)] = <em>value</em>]... {#modifygraph-for-axes}

</div>

This section of ModifyGraph relates to modifying the appearance of axes in a graph.

### *Parameters* {#modifygraph-for-axes-parameters}
Each parameter has the syntax:

*key* [(*axisName*)] = *value*

Each *key* parameter may take an optional *axisName* (abbreviated as *ax* in the synopsis above) enclosed in parentheses. *axisName* is "left", "right", "top", "bottom" or the name of an free axis such as "vertCrossing". For instance, "ModifyGraph axThick(left)=0.5" sets the axis thickness for only the left axis.

If "(*axisName*)" is omitted, all axes in the graph are affected. For instance, "ModifyGraph standoff=0" disables axis standoff for all axes in the graph.

The parameter descriptions below omit the optional "(*axisName*)" .


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">axisClip = *c*</span> | Specifies one of three clipping modes for traces. |
|  |<table class="nested-table"><tbody><tr><td>*c*&nbsp;=0:</td><td>Clips traces to a plot rectangle as defined by the pair of axes used by a given trace (default).</td></tr><tr><td>*c*&nbsp;=1:</td><td>Plots traces on an axis with a restricted range (as set by axisEnab) to extend to the full range of the normal plot rectangle.</td></tr><tr><td>*c*&nbsp;=2:</td><td>Traces extend outside the normal plot rectangle to the full extent of the graph area.</td></tr></tbody></table>
| <span class="table-cell-nowrap">axisEnab = {*lowFrac*,*highFrac*}</span> |  |
|  | Restricts the length of an axis to a subrange of normal. The axis is drawn from *lowFrac* to *highFrac* of graph area height (if axis is vertical) or width (if axis is horizontal). For instance, {0.1,0.75} specifies that the axis is drawn from 10% to 75% of the graph area height/width, instead of the normal 0% to 100%. AxisEnab is discussed in [Creating Split Axes](/igorpro/graphing/graphs.md#creating-split-axes) and [Creating Stacked Plots](/igorpro/graphing/graphs.md#creating-stacked-plots) in the Graphs help file. |
| <span class="table-cell-nowrap">axisOnTop = *t*</span> | Specifies drawing level of an axis and associated grid lines. |
|  |<table class="nested-table"><tbody><tr><td>*t*&nbsp;=0:</td><td>Draws axis before traces and images (default).</td></tr><tr><td>*t*&nbsp;=1:</td><td>Draws the axis after all traces and images.</td></tr></tbody></table>
| <span class="table-cell-nowrap">axOffset = *a*</span> | Specifies the distance from default axis position to actual axis position in units of the width of a zero character (0) in a tick mark label. Unlike margin, axOffset adjusts to changes in the size of the graph. |
| <span class="table-cell-nowrap">axThick = *t*</span> | Specifies the axis thickness in points. |
| <span class="table-cell-nowrap">barGap = *fraction*</span> | Sets the fraction of the width available for bars to be used as gap between bars. |
|  | barGap sets the gap between bars in a single category while catGap sets the gap between categories. |
| <span class="table-cell-nowrap">btLen = *p*</span> | Sets the length of major ("big") tick marks to *p* points. If *p* is zero, Igor uses the default length. *p* may be fractional. |
| <span class="table-cell-nowrap">btThick = *p*</span> | Sets the thickness of major ("big") tick marks to *p* points. If *p* is zero, Igor uses the default thickness. *p* may be fractional. |
| <span class="table-cell-nowrap">catGap = *fraction*</span> | The value for catGap is the fraction of the category width to be used as gap. The gap is divided equally between the start and end of the category width. A value of 0.2 would use 20% of the available space for the gap and leave 80% of the available space for the bars. |
|  | catGap sets the gap between categories while barGap sets the gap between bars in a single category. |
| <span class="table-cell-nowrap">dateFormat = {*languageName*, *yearFormat*, *monthFormat*, *dayOfMonthFormat*, *dayOfWeekFormat*, *layoutStr*, *commonFormat*}</span> |  |
|  | Sets the custom date format used in the active graph. |
|  | <div><Admonition type="note"><p>The custom date format is used only if you turn it on via a ModifyGraph dateInfo command. The last parameter to the ModifyGraph dateInfo command must be -1 to turn the custom date format on.</p></Admonition></div> |
|  | The parameters are the same as for the LoadWave/R flag except for the last one. |
|  | *commonFormat* selects the common date format to use in the Modify Axis dialog. The legal values correspond to the choices in the Common Format pop-up menu of the Modify Axis dialog. They are: |
|  |<table class="nested-table"><tbody><tr><td>**Value**</td><td>**Date Format**</td></tr><tr><td>1</td><td>mm/dd/yy</td></tr><tr><td>2</td><td>mm-dd-yy</td></tr><tr><td>3</td><td>mm.dd.yy</td></tr><tr><td>4</td><td>mmddyy</td></tr><tr><td>6</td><td>dd/mm/yy</td></tr><tr><td>7</td><td>dd-mm-yy</td></tr><tr><td>8</td><td>dd.mm.yy</td></tr><tr><td>9</td><td>ddmmyy</td></tr><tr><td>11</td><td>yy/mm/dd</td></tr><tr><td>12</td><td>yy-mm-dd</td></tr><tr><td>13</td><td>yy.mm.dd</td></tr><tr><td>14</td><td>yymmdd</td></tr><tr><td>16</td><td>mm/yy</td></tr><tr><td>17</td><td>mm.yy</td></tr><tr><td>18</td><td>Abbreviated month and year</td></tr><tr><td>19</td><td>Full month and year</td></tr><tr><td>21</td><td>mm/dd</td></tr><tr><td>22</td><td>dd.mm</td></tr><tr><td>23</td><td>Abbreviated month and day</td></tr><tr><td>24</td><td>Full month and day</td></tr><tr><td>26</td><td>Abbreviated date without day of week</td></tr><tr><td>27</td><td>Abbreviated date with day of week</td></tr><tr><td>28</td><td>Full date without day of week</td></tr><tr><td>29</td><td>Full date with day of week</td></tr></tbody></table>
|  | If the *commonFormat* parameter is negative, then it will select the Use Custom Format radio button in the Modify Axis dialog rather than Use Common Format and will then use the absolute value of *commonFormat* to determine which item in the Common Format pop-up menu to select. |
| <span class="table-cell-nowrap">dateInfo = {*sd*,*tm*,*dt*}</span> | Controls formatting of date/time axes. |
|  |<table class="nested-table"><tbody><tr><td>*sd*=0:</td><td>Show date in the date&amp;time format.</td></tr><tr><td>*sd*=1:</td><td>Suppress date.</td></tr><tr><td>*sd*=2:</td><td>Suppress time. The time is always shown if *tm*=2. *sd*=2 requires Igor Pro 9.00 or later.</td></tr><tr><td>*tm*=0:</td><td>12 hour (AM/PM) time.</td></tr><tr><td>*tm*=1:</td><td>24 hour (military) time.</td></tr><tr><td>*tm*=2:</td><td>Elapsed time.</td></tr><tr><td>*dt*=-1:</td><td>Custom date as specified via the dateFormat keyword.</td></tr><tr><td>*dt*=0:</td><td>Short dates (2/22/90).</td></tr><tr><td>*dt*=1:</td><td>Long dates (Thursday, February 22, 1990).</td></tr><tr><td>*dt*=2:</td><td>Abbreviated dates (Thurs, Feb 22, 1990).</td></tr></tbody></table>
| <span class="table-cell-nowrap">font = "*fontName*"</span> | Sets the axis label font, e.g., font(left)="Helvetica". |
| <span class="table-cell-nowrap">freePos(*freeAxName*) = *p*</span> |  |
|  | Sets the position of the free axis relative to the edge of the plot area to which the axis is anchored. *p* is in points, i.e., if the axis was made via /R=*axName* then the axis is placed *p* points from the right edge of the plot area. Positive is away from the central plot area. *freeAxName* may not be any of the standard axis names "left", "bottom", "right", or "top". |
| <span class="table-cell-nowrap">freePos(*freeAxName*) = {*crossAxVal*,*crossAxName*}</span> |  |
|  | Positions the free axis so it will cross the perpendicular  axis *crossAxName* where it has a value of *crossAxVal*. *freeAxName* may not be any of the standard axis names "left", "bottom", "right", or "top", though *crossAxName* may. |
|  | You can position a free axis as a fraction of the distance across the plot area by using kwFraction  for *crossAxName*. *crossAxVal* must then be between 0 and 1; any values outside this range are clipped to valid values. |
| <span class="table-cell-nowrap">fsize = *s*</span> | *s*=0 autosizes tick mark labels and axis labels. |
|  | If *s* is between 3 and 99 then the labels are fixed at *s* points. |
| <span class="table-cell-nowrap">fstyle = *f*</span> | *f* is a bitwise parameter with each bit controlling one aspect of the font style for the axis and tick mark labels as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">ftLen = *p*</span> | Sets the length of 5th (or emphasized minor) tick marks to *p* points. If *p* is zero, Igor uses the default length. *p* may be fractional. |
| <span class="table-cell-nowrap">ftThick = *p*</span> | Sets the thickness of 5th (or emphasized minor) tick marks to *p* points. If *p* is zero, Igor uses the default thickness. *p* may be fractional. |
| grid=*g* |<table class="nested-table"><tbody><tr><td>*g*&nbsp;=0:</td><td>Grid off.</td></tr><tr><td>*g*&nbsp;=1:</td><td>Grid on.</td></tr><tr><td>*g*&nbsp;=2:</td><td>Grid on major ticks only.</td></tr></tbody></table>
| <span class="table-cell-nowrap">gridEnab = {*lowFrac*,*highFrac*}</span> |  |
|  | Restricts the length of axis grid lines to a subrange of normal. The grid is drawn from *lowFrac* to *highFrac* of graph area height (if axis is horizontal) or width (if axis is vertical). |
| <span class="table-cell-nowrap">gridHair = *h*</span> | *h* =0 to 3, 0 for thicker lines, 3 for thinner. Default is 2. If h=0, the thickness of grid lines on major tick marks is the same as the axis thickness, half for a minor tick and one tenth for a subminor tick (log axis only). As h increases these thicknesses decrease by a factor of 2^h. If you want to see the effect of different values of gridHair, you will need to print a sample graph because you generally can't see the effect of thin lines on the screen. Also see the example experiment "Examples:Graphing Techniques:Graph Grid Demo". |
| <span class="table-cell-nowrap">gridStyle = *g*</span> | Sets the grid style to various combinations of solid and dashed lines. In the following discussion, major, minor and subminor refer to grid lines the corresponding tick marks. Subminor ticks are used only on log axes when there is a small range and sufficient room (they correspond to hundredths of a decade). The different grid styes are solid, dotted, dashed, and blank. The possible grids are as follows: |
|  |<table class="nested-table"><tbody><tr><td>*g*&nbsp;=0:</td><td>Same as mode 1 if graph background is white else uses mode 5.</td></tr><tr><td>*g*&nbsp;=1:</td><td>Major dotted, minor &amp; subminor dashed.</td></tr><tr><td>*g*&nbsp;=2:</td><td>All dotted.</td></tr><tr><td>*g*&nbsp;=3:</td><td>Major solid, minor dotted, subminor blank.</td></tr><tr><td>*g*&nbsp;=4:</td><td>Major &amp; minor solid, subminor dotted.</td></tr><tr><td>*g*&nbsp;=5:</td><td>All solid.</td></tr></tbody></table>
|  | Also see the example experiment "Examples:Graphing Techniques:Graph Grid Demo". |
| <span class="table-cell-nowrap">highTrip = *h*</span> | If the extrema of an axis are between its lowTrip and its highTrip then tick mark labels use fixed point notation. Otherwise they use exponential (scientific or engineering) notation. |
| <span class="table-cell-nowrap">lblLatPos = *p*</span> | Sets a lateral offset for the axis label. This is an offset parallel to the corresponding axis. *p* is in points. Positive is down for vertical axes and to the right for horizontal axes. |
| <span class="table-cell-nowrap">lblLineSpacing = *lineSpace*</span> |  |
|  | Specifies an adjustment to the normal line spacing for multi-line axis labels. |
|  | *lineSpace* is the amount of extra line spacing in points. It can be positive, zero or negative. |
|  | lblLineSpacing affects all lines of the axis label. See also the \sa and \sb escape codes described under [General Escape Codes](/igorpro/graphing/annotations.md#general-escape-codes). They can be used to affect the spacing between individual lines. |
| <span class="table-cell-nowrap">lblMargin = *l*</span> | Specifies the distance from edge of graph to label in points. |
| <span class="table-cell-nowrap">lblPos = *p*</span> | Sets the distance from an axis to the corresponding axis label in points. If *p* =0, it automatically picks an appropriate distance. |
|  | This setting is used only if the given graph edge has at least one free axis. Otherwise, the lblMargin setting is used to position the axis label. |
| <span class="table-cell-nowrap">lblPosMode = *m*</span> | Affects the meaning and usage of lblPos, lblLatPos and lblMargin parameters. Mainly for use when you have multiple axes on a side and you need axis labels to be properly positioned even as you make graph windows dramatically larger or smaller. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Default compatibility mode (Margin or Axis absolute depending on presence of free axis).</td></tr><tr><td>*m*&nbsp;=1:</td><td>Margin absolute.</td></tr><tr><td>*m*&nbsp;=2:</td><td>Margin scaled.</td></tr><tr><td>*m*&nbsp;=3:</td><td>Axis absolute.</td></tr><tr><td>*m*&nbsp;=4:</td><td>Axis scaled.</td></tr></tbody></table>
|  | The absolute modes are measured in Points whereas scaled modes have similar values but automatically expand or contract as the font height for the axis changes. Mode 0 is the default and results in no change relative to previous versions of Igor Pro that used lblMargin unless a given side used a free axis in which case it used lblPos in absolute mode. The margin modes measure relative to an edge of the graph while the axis modes measure relative to the position of the axis. When using stacked axes, use either margin modes. With multiple nonstacked axes, use Axis scaled if the graph edge is not using a fixed margin or use axis absolute if it is. |
| <span class="table-cell-nowrap">lblRot = *r*</span> | Rotates the axis label by *r* degrees. *r* is a value from -360 to 360. Rotation is counterclockwise and starts from the label's normal orientation. |
| <span class="table-cell-nowrap">linTkLabel = *tl*</span> | *tl* = 1 attaches to each tick label on a normal axis the data units with any exponent or prefix. *tl* =0 removes them. |
|  | In Igor Pro 9.00 and later, *tl*=2 suppresses the space character normally displayed before units. |
| log=*l* |<table class="nested-table"><tbody><tr><td>*l*&nbsp;=0:</td><td>Normal axis.</td></tr><tr><td>*l*&nbsp;=1:</td><td>Log base 10.</td></tr><tr><td>*l*&nbsp;=2:</td><td>Log base 2.</td></tr></tbody></table>
| <span class="table-cell-nowrap">logHTrip = *h*</span> | Same as highTrip but for log axes. |
| <span class="table-cell-nowrap">logLabel = *l*</span> | *l* is maximum number of decades in log axis before minor tick labels are suppressed. |
| <span class="table-cell-nowrap">logLTrip = *l*</span> | Same as lowTrip but for log axes. |
| <span class="table-cell-nowrap">loglinear = *l*</span> | Used with a log axis. *l* = 1 switches to a linear tick method if the number of decades of ranges is less than 2. It switches to a linear tick exponent method if the number of decades is greater than five. |
| <span class="table-cell-nowrap">logmtlOffset = *o*</span> | Offsets the minor tick mark labels on a log axis by *o* fractional points relative to the default tick mark label position. Positive is away from the axis. Added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">logTicks = *t*</span> | *t* is maximum number of decades in log axis before minor ticks are suppressed. |
| <span class="table-cell-nowrap">lowTrip = *l*</span> | If the extrema of an axis are between its lowTrip and its highTrip then tick mark labels use fixed point notation. Otherwise they use exponential (scientific or engineering) notation. |
| <span class="table-cell-nowrap">manminor = {*number*, *emphasizeEvery*}</span> |  |
|  | In manual tick mode, specifies how to draw minor ticks. There will be *number* ticks between each major (labeled) tick. You will usually want to set this to 4 to make 5 divisions, or 9 to make 10 divisions. A medium-sized tick (an emphasized minor tick) will be drawn every *emphasizeEvery* minor tick. |
| <span class="table-cell-nowrap">manTick = {*cantick*, *tickinc*, *exp*, *digitsrt* [, *timeUnit*]}</span> |  |
|  | Turns on manual tick mode. The tick from which all other ticks are calculated is the cononic tick (*cantick*). The numerical spacing between ticks is set by *tickinc*. cantick and tickinc are multiplied by 10<sup>exp</sup>. The number of digits to the right of the decimal point displayed in the tick labels is set by *digitsrt*. |
|  | The optional parameter*timeUnit* is used with Date/Time axes to specify the units of *tickinc*. In this case, *tickinc* must be an integer. The value of *timeUnit* is a keyword as follows: |
|  | `second` |
|  | `minute` |
|  | `hour` |
|  | `day` |
|  | `week` |
|  | `month` |
|  | `year` |
|  | On a date/time axis, the *exp* and *digitsrt* keywords are ignored, but must be present. You can set them to zero. |
| <span class="table-cell-nowrap">manTick = 0</span> | Turns off manual tick mode. |
| <span class="table-cell-nowrap">margin = *m*</span> | *m* is a fixed margin from the edge of the window to the axis in points. Used principally to make axes of multiple graphs on a page line up when "stacked". You can use the left, right, bottom, and top axis names (even if an axis with that name doesn't exist) to adjust the graph's plot area. See [Types of Axes](/igorpro/graphing/graphs.md#types-of-axes). |
|  |<table class="nested-table"><tbody><tr><td>*m*=0:</td><td>Sets &quot;automatic&quot; margin size (dependent on the length and height of tick marks and labels).</td></tr><tr><td>*m*=-1:</td><td>Sets the margin to &quot;none&quot;, or 0. The axis is drawn at the graph window&#39;s edge.</td></tr></tbody></table>
| minor=*m* |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Disables minor ticks.</td></tr><tr><td>*m*&nbsp;=1:</td><td>Enables minor ticks.</td></tr></tbody></table>
| mirror=*m* |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>No mirroring.</td></tr><tr><td>*m*&nbsp;=2:</td><td>Mirror axis without tick marks.</td></tr><tr><td>*m*&nbsp;=3:</td><td>Mirror axis with tick marks and tick labels.</td></tr><tr><td>*m*&nbsp;=1:</td><td>Right axis mirroring left or top mirroring bottom.</td></tr></tbody></table>
| <span class="table-cell-nowrap">mirrorPos = *pos*</span> | Specifies the position of the mirror axis relative to the normal position. *pos* is a value between 0 and 1. |
| noLabel=*n* |<table class="nested-table"><tbody><tr><td>*n*&nbsp;=0:</td><td>Normal labels.</td></tr><tr><td>*n*&nbsp;=1:</td><td>Suppress tick mark labels.</td></tr><tr><td>*n*&nbsp;=2:</td><td>Suppress tick mark labels and axis labels.</td></tr></tbody></table>
| notation=*n* |<table class="nested-table"><tbody><tr><td>*n*&nbsp;=0:</td><td>Engineering notation.</td></tr><tr><td>*n*&nbsp;=1:</td><td>Scientific notation.</td></tr></tbody></table>
|  | Affects tick mark labels displayed exponentially. See highTrip and lowTrip. |
|  | Does not affect log axes. |
| <span class="table-cell-nowrap">nticks = *n*</span> | *n* =approximate number of ticks marks on axis. |
| <span class="table-cell-nowrap">prescaleExp = *exp*</span> | Multiplies axis range by 10^*exp* for tick labeling and *exp* is subtracted from the axis label exponent. In other words, the exponent is moved from the tick labels to the axis label. (This affects the display only, not the source data.) |
| <span class="table-cell-nowrap">sep = *s*</span> | *s* =minimum number of screen pixels between minor ticks. |
| standoff=*s* |<table class="nested-table"><tbody><tr><td>*s*&nbsp;=0:</td><td>Suppresses axis standoff.</td></tr><tr><td>*s*&nbsp;=1:</td><td>Enables standoff.</td></tr></tbody></table>
|  | Axis standoff prevents waves or markers from covering the axis. |
| <span class="table-cell-nowrap">stLen = *p*</span> | Sets the length of minor ("small") tick marks to *p* points. If *p* is zero, Igor uses the default length. *p* may be fractional. |
| <span class="table-cell-nowrap">stThick = *p*</span> | Sets the thickness of minor ("small") tick marks to *p* points. If *p* is zero, Igor uses the default thickness. *p* may be fractional. |
| <span class="table-cell-nowrap">tick = *t*</span> | Sets tick position. |
|  |<table class="nested-table"><tbody><tr><td>*t*&nbsp;=0:</td><td>Outside axis.</td></tr><tr><td>*t*&nbsp;=1:</td><td>Crossing axis.</td></tr><tr><td>*t*&nbsp;=2:</td><td>Inside axis.</td></tr><tr><td>*t*&nbsp;=3:</td><td>None.</td></tr></tbody></table>
|  | In a category plot, adding 4 to the usual values for the tick keyword will place the tick marks in the center of each category rather than at the edges. |
|  | In a normal (non-category) plot specifying *t*=4 or *t*=5 replaces tick marks and axis lines with rectangular regions with alternating fills. This feature, which was added in Igor Pro 8.00, is used for cartographic plots. |
|  | *t*=4 gives even fills and *t*=5 gives odd fills. The btLen keyword determines the thickness of the fill area. |
|  | It is recommended that you use mirror axes and axisOnTop=1 as shown in this example: |
|  | <code class="igor">Make jack=sin(x/8)&#10;Display jack&#10;ModifyGraph axisOnTop=1&#10;ModifyGraph mirror=1&#10;ModifyGraph standoff=0&#10;ModifyGraph tick=4</code> |
| <span class="table-cell-nowrap">tickEnab = {*lowTick*,*highTick*}</span> |  |
|  | Restricts axis ticking to a subrange of normal. Ticks are drawn and labelled only if they fall within this inclusive numerical range. |
| <span class="table-cell-nowrap">tickExp = *te*</span> | *te* =1 forces tick labels to exponential notation when labels have units with a prefix. *te* =0 turns this off. |
| <span class="table-cell-nowrap">tickUnit = *tu*</span> | *tu* = 1 suppresses units labels attached to tick marks. *tu* =0 turns them back on. |
| <span class="table-cell-nowrap">tickZap = {[*v1* [, *v2* [, *v3*]]]}</span> |  |
|  | Suppresses drawing of the tick mark label for values given in the list. This is useful when you have crossing axes to prevent tick mark labels from overlapping. The list may contain zero, one, two or three values. The values must be exact to suppress the label. |
| <span class="table-cell-nowrap">tkLblRot = *r*</span> | Rotates the tick mark labels by *r* degrees. *r* is a value from -360 to 360. Rotation is counterclockwise and starts from the label's normal orientation. |
| <span class="table-cell-nowrap">tlOffset = *o*</span> | Offsets the tick mark labels by *o* fractional points relative to the default tick mark label position. Positive is away from the axis. |
| <span class="table-cell-nowrap">ttLen = *p*</span> | Sets the length of subminor ("tiny") tick marks to *p* points. If *p* is zero, Igor uses the default length. *p* may be fractional. Subminor ticks are used only in log axes. |
| <span class="table-cell-nowrap">ttThick = *p*</span> | Sets the thickness of subminor ("tiny") tick marks to *p* points. If *p* is zero, Igor uses the default thickness. *p* may be fractional. |
| <span class="table-cell-nowrap">userticks = {*tickPosWave*,*tickLabelWave*}</span> |  |
|  | Draws axes with purely user-defined tick mark positions and labels, overriding other settings. *tickPosWave* is a numeric wave containing the desired positions of the tick marks, and *tickLabelWave* is a text wave containing the labels. See [User Ticks from Waves](/igorpro/graphing/graphs.md#user-ticks-from-waves) for an example. |
|  | The tick mark labels can be multiline and use styled text. For more details, see [Fancy Tick Mark Labels](/igorpro/graphing/category-plots.md#fancy-tick-mark-labels). |
|  | *tickPosWave* need not be monotonic. Igor will plot a tick if a value is in the range of the axis. Both linear and log axes are supported. |
|  | Graph margins will adjust to accommodate the size of tick labels. This will not prevent overlap between labels, which you will need fix yourself. |
| <span class="table-cell-nowrap">userticks = 0</span> | Removes the userticks setting returning the axis to the previously-set mode previously. |
| <span class="table-cell-nowrap">useTSep = *t*</span> | *t* =1 displays a thousand's separator character between every group of three digits in the tick mark label (e.g., "1,000" instead of "1000"). The default is *t* =0. |
| <span class="table-cell-nowrap">zapLZ = *t*</span> | *t* =1 removes leading zeros from tick mark labels. For example 0.5 becomes .5 and -0.5 becomes -.5. The default is *t* =0. |
| <span class="table-cell-nowrap">zapTZ = *t*</span> | *t* =1 removes trailing zeros from tick mark labels. The radix point will also be removed if all digits are zero. Default is *t* =0. |
| zero=*z* |<table class="nested-table"><tbody><tr><td>*z*&nbsp;=0:</td><td>No zero line (the default).</td></tr><tr><td>*z*&nbsp;=1:</td><td>A zero line at x=0 or y=0.</td></tr><tr><td></td><td>The line style is set to z-1. See [ModifyGraph for Traces](#modifygraph-for-traces), lStyle keyword, for details on line styles.</td></tr></tbody></table>
| <span class="table-cell-nowrap">zeroThick = *zt*</span> | Sets the thickness of the zero line in points, from 0.0 to 5.0 points. *zt* =0.0 means the zero line thickness automatically follows the thickness of the axis; this is the default. You can use 0.1 for a thin zero line thickness. |
| <span class="table-cell-nowrap">ZisZ = *t*</span> | *t* =1 uses the single digit 0 as the zero tick mark label (if any) regardless of the number of digits used for other labels. Default is *t* =0. |

### *Flags* {#modifygraph-for-axes-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Modifies the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/Z</span> | Does not generate an error if the named axis does not exist in a style macro. |

### *Details* {#modifygraph-for-axes-details}
With the prescaleExp parameter, you can force tick and axis label scaling to values different from the defaults. For example, if you have data whose X scaling ranges from 9pA to 120pA and you display this on a log axis, the tick marks will be labelled 10pA and 100pA. But if you really want the tick marks labeled 10 and 100 with pA in the axis label, you can set the prescaleExp to 12. To see this, execute the following commands:


```igor
Make/O jack=x
Display jack
SetScale x,9e-12,120e-12,"A",jack
ModifyGraph log(bottom)=1
```

then execute:


```igor
ModifyGraph prescaleExp(bottom)=12
```

The tickExp parameter applies to units that do not traditionally use SI prefix characters. For example, one usually speaks of 10^-3 Torr and not mTorr. To see how this feature works, execute the following example commands:


```igor
Make/O jack=x
Display jack
SetScale x,1E-7,1E-5,"Torr",jack
ModifyGraph log(bottom)=1
```

then execute:


```igor
ModifyGraph tickExp(bottom)=1
```

at this point, the tick mark labels have Torr in them. If you want to eliminate the units from the tick marks, execute:


```igor
ModifyGraph tickUnit(bottom)=1
```

and if you now want Torr in the label string, use the \U escape in the label string:


```igor
Label bottom "\\U"
```

To see the effect of linTkLabel, execute these commands:


```igor
Make/O jack=x
Display jack
SetScale x,1E-7,1E-5,"Torr",jack
```

then execute:


```igor
ModifyGraph linTkLabel(bottom)=1
```

and then try:


```igor
ModifyGraph tickExp(bottom)=1
```

and finally:


```igor
ModifyGraph tickUnit(bottom)=1
```

### *See Also* {#modifygraph-for-axes-see-also}
[ModifyGraph](/igorpro/commands/modifygraph.md) (General settings)

[ModifyGraph for Traces](#modifygraph-for-traces)

[ModifyGraph for Colors](#modifygraph-for-colors)

### *Demos* {#modifygraph-for-axes-demos}
[Open Graph Grid Demo](#igor-pxp/Examples/Feature__Demos__2/Graph__Grid__Demo.pxp)



<!-- IndentedSubtopic -->
## ModifyGraph for Colors {#modifygraph-for-colors}

<div className="command-signature">

## <strong>ModifyGraph</strong>  [/W=<em>winName</em> /Z] [<em>keyword</em>=<em>value</em>, <em>keyword</em>=<em>value</em>, ...] {#modifygraph-for-colors}

</div>

This section of ModifyGraph relates to modifying the use of colors in a graph.

### *Parameters* {#modifygraph-for-colors-parameters}
Most of the key parameters may take an optional *axisName* (abbreviated as *ax* in the synopsis above) enclosed in parentheses. *axisName* is "left", "right", "top", "bottom" or the name of an free axis such as "vertCrossing".

Where the parameter descriptions indicate an "(*axisName*)", it may be omitted to change all axes in the graph.

*r*, *g,* *b,* and *a* specify the color and opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). (0,0,0) specifies opaque black and (65535,65535,65535) specifies opaque white.


| Parameter Specification | Object Colored |
| --- | --- |
| <span class="table-cell-nowrap">alblRGB(*axisName*) = (*r*,*g*,*b*[,*a*])</span> | Axis labels |
| <span class="table-cell-nowrap">axRGB(*axisName*) = (*r*,*g*,*b*[,*a*])</span> | Axis |
| <span class="table-cell-nowrap">cbRGB = (*r*,*g*,*b*[,*a*])</span> | Control bar background |
| gbGradient | See [Gradient Fills](/igorpro/graphing/making-figures/graphics.md#gradient-fills) for parameters and details. |
| gbGradientExtra | See [Gradient Fills](/igorpro/graphing/making-figures/graphics.md#gradient-fills) for parameters and details. |
| <span class="table-cell-nowrap">gbRGB = (*r*,*g*,*b*[,*a*])</span> | Graph background |
| <span class="table-cell-nowrap">gridRGB(*axisName*) = (*r*,*g*,*b*[,*a*])</span> | Axis grid lines |
| <span class="table-cell-nowrap">tickRGB(*axisName*) = (*r*,*g*,*b*[,*a*])</span> | Axis tick marks |
| <span class="table-cell-nowrap">tlblRGB(*axisName*) = (*r*,*g*,*b*[,*a*])</span> | Axis tick labels |
| wbGradient | See [Gradient Fills](/igorpro/graphing/making-figures/graphics.md#gradient-fills) for parameters and details. |
| wbGradientExtra | See [Gradient Fills](/igorpro/graphing/making-figures/graphics.md#gradient-fills) for parameters and details. |
| <span class="table-cell-nowrap">wbRGB = (*r*,*g*,*b*[,*a*])</span> | Window background |

### *Flags* {#modifygraph-for-colors-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Modifies the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/Z</span> | Does not generate an error if the named axis does not exist in a style macro. |

### *Details* {#modifygraph-for-colors-details}
On Windows, use maximum white to set the control bar background color to track the 3D Objects color in the Appearance Tab of the Display Properties control panel:


```igor
ModifyGraph cbRGB=(65535,65535,65535)
```

### *See Also* {#modifygraph-for-colors-see-also}
[ModifyGraph](/igorpro/commands/modifygraph.md) (General settings)

[ModifyGraph for Traces](#modifygraph-for-traces)

[ModifyGraph for Axes](#modifygraph-for-axes)

[Controls in Graphs](/igorpro/user-interface/controls.md#controls-in-graphs)