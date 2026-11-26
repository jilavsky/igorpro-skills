---
description: "The Interpolate2 operation performs linear, cubic spline and smoothing cubic spline interpolation on 1D waveform or XY data."
slug: /commands/interpolate2
---

<div className="command-signature">

## <strong>Interpolate2</strong>  [<em>flags</em> ] [ <em>xWave</em> , ] <em>yWave</em> {#interpolate2}

</div>

The Interpolate2 operation performs linear, cubic spline and smoothing cubic spline interpolation on 1D waveform or XY data. It produces output in the form of a waveform or an XY pair.

The cubic spline interpolation is based on a routine from "Numerical Recipes in C".

The smoothing spline is based on "Smoothing by Spline Functions", Christian H. Reinsch, *Numerische Mathematic* 10, 177-183 (1967).

For background information, see [The Interpolate2 Operation](/igorpro/analysis/analysis.md#the-interpolate2-operation).

### *Parameters* {#parameters}
*xWave* specifies the wave which supplies the X coordinates for the input curve. If you omit it, X coordinates are taken from the X values of *yWave*.

*yWave* specifies the wave which supplies the Y coordinates for the input curve.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = *a*</span> | Controls pre-averaging. Pre-averaging is deprecated - use the smoothing spline (/T=3) instead. |
|  | If *a* is zero, Interpolate2 does no pre-averaging. If *a* is greater than one, it specifies the number of nodes through which you want the output curve to go. Interpolate2 creates the nodes by averaging the raw input data. |
|  | Pre-averaging does not work correctly with the log-spaced output mode (/I=2). This is because the pre-averaging is done on linearly-spaced intervals but the input data is log-spaced. |
| <span class="table-cell-nowrap">/E = *e*</span> | Controls how the end points are determined for cubic spline interpolation only. |
|  |<table class="nested-table"><tbody><tr><td>*e*&nbsp;=1:</td><td>Match first derivative (default)</td></tr><tr><td>*e*&nbsp;=2:</td><td>Match second derivative (natural)</td></tr></tbody></table>
| <span class="table-cell-nowrap">/F = *f*</span> | *f* is the smoothing factor used for the smoothing spline. |
|  | *f* =0 is nearly identical to the cubic spline. |
|  | *f* >0 gives increasing amounts of smoothing as *f* increases. |
|  | See [Smoothing Spline Parameters](/igorpro/analysis/analysis.md#smoothing-spline-parameters) for details. |
| <span class="table-cell-nowrap">/FREE</span> | Creates output waves as free waves (see [Free Waves](/igorpro/programming/programming.md#free-waves)). |
|  | /FREE is allowed only in functions. If you use /FREE then the output waves specified by /X and /Y must be either simple names or valid wave references. |
|  | /FREE was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/I[ = i]</span> | Determines at what X coordinates the interpolation is done. |
|  |<table class="nested-table"><tbody><tr><td>*i*&nbsp;=0:</td><td>Gives output values at evenly-spaced X coordinates that span the X range of the input data. This is the default setting if /I is omitted.</td></tr><tr><td>*i*&nbsp;=1:</td><td>Same as i=0 except that the X input values are included in the list of X coordinates at which to interpolate. This is rarely needed and is not available if no X destination wave is specified. /I is equivalent to /I=1. Both are not recommended.</td></tr><tr><td>*i*&nbsp;=2:</td><td>Gives output values at X coordinates evenly-spaced on a logarithmic scale. Use this if your data is plotted on a logarithmic X axis. Ignores any non-positive values in your input X data.</td></tr><tr><td></td><td>This mode is not recommended. See [Interpolating Exponential Data](/igorpro/analysis/analysis.md#interpolating-exponential-data) for an alternative.</td></tr><tr><td>*i*&nbsp;=3:</td><td>Gives output values at X coordinates that you specify by setting the X coordinates of the destination wave before calling Interpolate2. You must create your destination wave or waves before doing the interpolation for this mode.</td></tr></tbody></table>
|  | If you omit /X=*xDest* then the X coordinates come from the X values of the output waveform designated by /Y=*yDest* . |
|  | If you include /X=*xDest* then the X coordinates come from the data values of the specified X output wave. |
|  | When using /I=3, the number of output points is determined by the destination wave and the /N flag is ignored. |
|  | See [Destination X Coordinates from Destination Wave](/igorpro/analysis/analysis.md#destination-x-coordinates-from-destination-wave) for further details. |
| <span class="table-cell-nowrap">/J = *j*</span> | Controls the use of end nodes with pre-averaging (/A). Pre-averaging is deprecated - use the smoothing spline (/T=3) instead. |
|  |<table class="nested-table"><tbody><tr><td>*j*&nbsp;=0:</td><td>Turns end nodes off.</td></tr><tr><td>*j*&nbsp;=1:</td><td>Creates end nodes by cubic extrapolation.</td></tr><tr><td>*j*&nbsp;=2:</td><td>Creates end nodes equal to the first and last data points of the input data set, not counting points that contain NaNs or INFs.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/N = *n*</span> | Controls the number of points in the output wave or waves. *n* defaults to the larger of 200 and the number of points in the source waves. This value is ignored if you /I=3 (X from dest mode). |
| <span class="table-cell-nowrap">/S = *s*</span> | *s* is the estimated standard deviation of the noise of the Y data. It is used for the smoothing spline only. *s* is used as the estimated standard deviation for all points in the Y data. |
|  | If neither /S nor /SWAV are present, Interpolate2 arbitrarily assumes an *s* equal to .05 times the amplitude of the Y data. |
| <span class="table-cell-nowrap">/SWAV = *stdDevWave*</span> | *stdDevWave* is a wave containing the standard deviation of the noise of the Y data on a point-by-point basis. It is used for the smoothing spline only. *stdDevWave* must have the same number of points as the Y data wave. |
|  | If neither /S nor /SWAV are present, Interpolate2 arbitrarily assumes an *s* equal to .05 times the amplitude of the Y data. |
| <span class="table-cell-nowrap">/T = *t*</span> | Controls the type of interpolation performed. |
|  |<table class="nested-table"><tbody><tr><td>*t*&nbsp;=1:</td><td>Linear interpolation</td></tr><tr><td>*t*&nbsp;=2:</td><td>Cubic spline interpolation (default)</td></tr><tr><td>*t*&nbsp;=3:</td><td>Smoothing spline interpolation</td></tr></tbody></table>
| <span class="table-cell-nowrap">/X = *xDest*</span> | Specifies the X destination wave name. |
|  | If /X is present the output is an XY pair. |
|  | If /X is omitted the output is a waveform. |
|  | The X destination wave may or may not exist when Interpolate2 is called except for "X from dest" mode (/I=3) when it must exist. Interpolate2 overwrites it if it exists. |
| <span class="table-cell-nowrap">/Y = *yDest*</span> | Specifies the Y destination wave name. |
|  | If you omit /Y, a default wave name is generated. The name of the default wave is the name of the source Y wave plus "_L" for linear interpolation, "_CS" for cubic spline or "_SS" for smoothing spline. |
|  | The Y destination wave may or may not exist when Interpolate2 is called. Interpolate2 overwrites it if it exists. |

### *See Also* {#see-also}
[The Interpolate2 Operation](/igorpro/analysis/analysis.md#the-interpolate2-operation)

### *Demos* {#demos}
[Open Interpolate2 Log Demo](#igor-pxp/Examples/Feature__Demos/Interpolate2__Log__Demo.pxp)

### *References* {#references}
"*Numerical Recipes in C* " for cubic spline.

"Smoothing by Spline Functions", Christian H. Reinsch, *Numerische Mathematic* 10, 177-183 (1967).