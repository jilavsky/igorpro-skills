---
description: "The ErrorBars operation adds or removes error bars to or from the named trace in the specified graph and modifies error bar settings."
slug: /commands/errorbars
---

<div className="command-signature">

## <strong>ErrorBars</strong>  [/W=<em>winName</em> /CLIP=<em>clip</em> /L=<em>lineThick</em> /T=<em>thick</em> /X=<em>xWidth</em> /Y=<em>yWidth</em> /RGB=<em>strokeColor</em> ] <em>traceName</em>, <em>mode</em> [<em>errorSpecification</em> [, <em>errorSpecification</em>] ] {#errorbars}

</div>

The ErrorBars operation adds or removes error bars to or from the named trace in the specified graph and modifies error bar settings.

The most common format is "error bars": lines that extend from each data point to "caps". The length of the line (or "bar") is usually used to bracket a measured value by the amount of uncertainty, or "error" in the measurement.

Error bars can extend in the horizontal or vertical direction or both. They may be symmetric or asymmetric.

Errors may also be shown by a box that represents errors in both directions, by a semi-transparent band (vertical errors only) or by error ellipses.

### *Parameters* {#parameters}
*traceName* is the name of a trace on a graph (see [Trace Names](/igorpro/graphing/graphs.md#trace-names)).

A string containing *traceName* can be used with the $ operator to specify *traceName*.

*mode* is one of the following keywords:

|  |  |
| --- | --- |
| OFF | No error bars. |
| X | Horizontal error bars only. |
| Y | Vertical error bars only. |
| XY | Horizontal and vertical error bars. |
| <span class="table-cell-nowrap">BOX [ = *fillColor*]</span> | Box error bars, optionally with fill color expressed as (r,g,b) or (r,g,b,a). If no color is specified, boxes are not filled. The *fillColor* parameter was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">ELLIPSE = {*mode*, *p*, *alpha*}</span> |  |
|  | Plots error ellipses. |
|  | You must provide error values via a three-column wave using the ewave=*ew* error specification described below. |
|  |<table class="nested-table"><tbody><tr><td>*mode*=0:</td><td>*ew* contains the standard deviation in X, the standard deviation in Y, and the correlation between X and Y.</td></tr><tr><td>*mode*=1:</td><td>*ew* contains the variance in X, the variance in Y, and the covariance of X and Y.</td></tr></tbody></table>
|  | *p* is the probability level represented by the error ellipses. *p*=0.6837, *p*=0.95, and *p*=0.997 represent one, two, and three standard deviations respectively. Larger values of *p* result in larger ellipses corresponding to higher confidence levels. |
|  | *alpha* is an opacity value in the range of 0 (fully transparent) to 65535 (fully opaque). See [Error Ellipse Color](/igorpro/graphing/graphs.md#error-ellipse-color) for details. |
|  | The ellipse mode was added in Igor Pro 9.00. |
|  | See [Error Ellipses](/igorpro/graphing/graphs.md#error-ellipses) for further discussion. |
| NOCHANGE | This mode allows you to programmatically change aspects of error bars using flags (see ***Flags*** below) without affecting the mode or error specification. The NOCHANGE mode was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">SHADE = {*options*, *fillMode*, *fgColor*, *bkColor* [ , *negFillMode*, *negFgColor*, *negBkColor* ]}</span> |  |
|  | SHADE was added in Igor Pro 7.00. |
|  | *options* is reserved for future use and must be zero. |
|  | *fillMode* sets the fill pattern: |
|  |<table class="nested-table"><tbody><tr><td>*fillMode*&nbsp;=0:</td><td>Solid black.</td></tr><tr><td>*fillMode*&nbsp;=1:</td><td>Solid black.</td></tr><tr><td>*fillMode*&nbsp;=2:</td><td>Solid black.</td></tr><tr><td>*fillMode*&nbsp;=3:</td><td>75% gray</td></tr><tr><td>*fillMode*&nbsp;=4:</td><td>50% gray</td></tr><tr><td>*fillMode*&nbsp;=5:</td><td>25% gray.</td></tr><tr><td>*fillMode*&nbsp;&gt;=6:</td><td>See [Fill Patterns](/igorpro/graphing/making-figures/graphics.md#fill-patterns).</td></tr></tbody></table>
|  | *fgColor* is (r,g,b) or (r,g,b,a). If all zeros including alpha, i.e., (0,0,0,0), then the actual color will be the trace color with an alpha of 20000. |
|  | *bkColor* is used for patterns only and can be simply (0,0,0) for solid fills. |
|  | *negFillMode* is the same as *fillMode* but for negative error shading. |
|  | *negFgColor* is the same as *fgColor* but for negative error shading. |
|  | *negBkColor* is the same as *bkColor* but for negative error shading. |
|  | The *errorSpecification*, described below, affects only the Y amplitude of error shading. |
|  | The X values of the trace to which shading is applied must be monotonic. Results with non-monotonic X values are undefined. |
|  | See [Error Shading](/igorpro/graphing/graphs.md#error-shading) for more information and examples. See [Color Blending](/igorpro/graphing/making-figures/graphics.md#color-blending) for information on the alpha color parameter. |

For any mode other than `OFF` and `NOCHANGE`, there is an error specification whose format is:


```igor
	keyword [=value]
```

### *Error Specification Parameters* {#error-specification-parameters}
For any mode other than `OFF` and `NOCHANGE`, you must provide an error specification which consists of a keyword followed by zero or more parameters:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">pct = *value*</span> | *value* is the length of an error bar expressed as a percentage of the trace X or Y value. |
| sqrt | The error bar length is the square root of the trace X or Y value. |
| <span class="table-cell-nowrap">const = *value*</span> | *value* is the length of an error bar independent of the trace X or Y value. |
| <span class="table-cell-nowrap">ewave = *ew*</span> | *ew* is a three-column wave with error ellipse parameters. Each row represents information for one trace data point. The interpretation of the columns of *ew* depends on the mode parameter provided with the ELLIPSE keyword: |
|  |<table class="nested-table"><tbody><tr><td>*mode*=0:</td><td>*ew* contains the standard deviation in X, the standard deviation in Y, and the correlation between X and Y.</td></tr><tr><td>*mode*=1:</td><td>*ew* contains the variance in X, the variance in Y, and the covariance of X and Y.</td></tr></tbody></table>
|  | *ew* may include a subrange specification as long as it results in effectively a 2D wave with three columns and a row for each trace data point. See [Subrange Display Syntax](/igorpro/graphing/graphs.md#subrange-display-syntax). |
|  | See [Error Ellipses](/igorpro/graphing/graphs.md#error-ellipses) for further discussion. |
| <span class="table-cell-nowrap">wave = (*w1*,*w2*)</span> | Each error bar length is obtained from the corresponding point of wave *w1* for positive bars and from *w2* for negative bars. |
|  | If you omit *w1* no positive bars are drawn. If you omit *w2* no negative bars are drawn. |
|  | You can use [Subrange Display Syntax](/igorpro/graphing/graphs.md#subrange-display-syntax) for *w1* and *w2*. |
| <span class="table-cell-nowrap">mulWave = *ew*</span> | Each error bar length is computed from a multiplier taken from the corresponding point of a wave *ew*.<br>If your trace wave is *tw*, the error bar lengths are computed as: |
|  | <code class="igor">positive error bar length = tw \* (ew - 1)</code> |
|  | <code class="igor">negative error bar length = tw \* (1 - 1/ew)</code> |
|  | This is appropriate if you have computed geometric mean and standard deviation, as would be appropriate for errors with lognormal distribution. Such error bars appear symmetrical on a log axis. |
|  | The values in *ew* must be greater than or equal to 1. Values less than 1 result in the error bar not being displayed for that data point. An error value of exactly 1 results in a zero-length error bar. |
|  | The mulWave keyword was added in Igor Pro 9.00. |
| nochange | The *errorSpecification* is unchanged from existing values. nochange allows you to, for instance, change the fill color for the box mode without having to repeat *errorSpecification* for the X and Y errors. nochange was added in Igor Pro 8.00. |

If the *mode* is `XY` or `BOX`, two error specifications are required, separated by a comma. Other modes require just one error specification; providing two results in an error.

See ***Examples*** below for examples using *mode* and *errorSpecification*.

*mode* and *errorSpecification* control only the lengths of the horizontal and vertical lines (the "bars") to the "caps". All other sizes and thicknesses are controlled by the flags.

<img src="Images/ErrorBars/ErrorBars_1.png" width="100%"/>

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/CLIP = *clip*</span> |  |
| <span class="table-cell-nowrap">/CLIP = {*clipH*, *clipV*}</span> | Sets a distance in points by which error bars are allowed to extend beyond the plot area. If you use the first form, the vertical and horizontal values are both set to *clip*. Use the second form to set horizontal and vertical clipping independently. *clipH* and *clipV* default to 2 points. Values may be negative to restrict error bar drawing to an area inside the plot area. /CLIP was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/L = *lineThick*</span> | *lineThick* is the thickness of both the X and Y error bars drawn from the point on the wave to the caps. If you use the `ELLIPSE` keyword to draw error ellipses, *lineThick* sets the thickness of the ellipse outline. |
| <span class="table-cell-nowrap">/RGB = *strokeColor*</span> | Sets the color of the lines used to draw the error bars. *strokeColor* is expressed as (r,g,b) or (r,g,b,a). The default color, used if you omit /RGB, is the same as the color of the trace to which the error bars are attached. The /RGB flag was added in Igor Pro 8.00. |
|  | If you use the `ELLIPSE` keyword, *strokeColor* sets the color of the ellipse outline. |
| <span class="table-cell-nowrap">/T = *thick*</span> | *thick* is the thickness of both the X and Y error bar "caps". In box mode, /T sets the thickness of the box outline. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Changes error bars in the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/X = *xWidth*</span> | *xWidth* is the width (height, actually) of the caps to the left or right of the point. |
| <span class="table-cell-nowrap">/Y = *yWidth*</span> | *yWidth* is the width of the caps above or below the point. |

The thicknesses and widths are in units of points. The thickness parameters need not be integers. Although only integral thicknesses can be displayed exactly on a standard resolution screen, nonintegral thicknesses are produced properly on high resolution devices. Use /T=0 to completely suppress the caps and /L=0 to completely suppress the lines to the caps.

### *Details* {#details}
If a wave specifying error values for *waveName* is shorter than *waveName* then the last value of the error wave is used for the unavailable points. If a point in an error wave contains NaN (Not a Number) then the half-bar associated with that point is not shown.

### *Examples* {#examples}

```igor
// X 10% of wave1, Y is 5% of wave1
ErrorBars wave1, XY pct=10, pct=5

// X error bars only, square root of wave1
ErrorBars wave1,X sqrt

// Y error bars only, constant error value = 4.3
ErrorBars wave1,Y const=4.3

// X and Y error bars, symmetric with X error from wave w1 and Y error from wave w2
ErrorBars wave1,XY wave=(w1, w1), wave=(w2, w2)

// Error box, 10% in horizontal direction, 5% in vertical direction
ErrorBars wave1,BOX pct=10,pct=5

// Error box filled with blue color having 50% alpha (transparency)
// 10% in horizontal direction, 5% in vertical direction
ErrorBars wave1,BOX=(0,0,65535,32767) pct=10,pct=5	

// Change the error box fill to red color having 50% alpha
// without changing the way the errors are computed.
ErrorBars wave1,BOX=(65535,0,0,32767) nochange, nochange

// Y error bars only, wave w1 has errors for Y+ bars
// wave w2 has errors for Y- bars
ErrorBars wave1,Y wave=(w1,w2)

// Y error bars only, same wave for both Y+ and Y-.
// Overrides the trace color to make the error bars black.
ErrorBars/RGB=(0,0,0) wave1,Y wave=(w1,w1)

// Y error bars only, no Y+ error bars, wave w2 has errors for Y- bars
ErrorBars wave1,Y wave=(,w2)

// Turns error bars for wave1 off
ErrorBars wave1,OFF
```

### *Error Ellipse Example* {#error-ellipse-example}
See [Error Ellipse Example](/igorpro/graphing/graphs.md#error-ellipse-example).

### *See Also* {#see-also}
[Error Bars](/igorpro/graphing/graphs.md#error-bars), [Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)