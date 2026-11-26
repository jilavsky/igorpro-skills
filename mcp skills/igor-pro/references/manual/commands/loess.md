---
description: "The Loess operation smooths srcWaveName using locally-weighted regression smoothing."
slug: /commands/loess
---

<div className="command-signature">

## <strong>Loess</strong>  [/CONF={<em>confInt</em>, <em>ciPlusWaveName</em> [,<em>ciMinusWaveName</em>]} /DEST=<em>destWaveName</em> /DFCT[={<em>destFactorWaveName1</em> [,<em>destFactorWaveName</em>...]}] /E=<em>extrapolate</em> /N=<em>neighbors</em>  /ORD=<em>order</em>  /PASS=<em>passes</em>  /R=<em>robust</em> /SMTH= <em>sf</em>  /TIME=<em>secs</em> /V=<em>verbose</em> /Z=<em>z</em> ] <em>srcWave</em>=<em>srcWaveName</em>  [, <em>factors</em>=<em>factorWaveName1</em> [, <em>factorWaveName2</em>...]] {#loess}

</div>

The Loess operation smooths *srcWaveName* using locally-weighted regression smoothing. This algorithm is sometimes classified as a "nonparametric regression" procedure. The regression can be constant, linear, or quadratic. A robust option that ignores outliers is available. See ***Basic Algorithm***, ***Robust Algorithm***, and ***References***, below, for additional details and terminology.

This implementation works with waveforms, XY pairs of waves, false-color images, matrix surfaces, and multivariate data (one dependent data wave with multiple independent variable data waves).

Unlike the [FilterFIR](/igorpro/commands/filterfir.md) operation, Loess discards any NaN input values and will not generate a result that is wholly NaN.

### *Parameters* {#parameters}
*srcWaveName* is the input data to be smoothed. It may be a one-dimensional or a two-dimensional wave, and it may contain NaNs.

When the /DEST flag is unspecified, Loess will overwrite *srcWaveName* with the smoothed result.

If *srcWaveName* is one-dimensional and no factors are provided, X values are derived from *srcWaveName* 's x scaling.

If *srcWaveName* is two-dimensional, the factors keyword is not permitted and the X and Y values are derived from *srcWaveName*'s X and Y scaling.

Higher dimensions of *srcWaveName* are not supported

The optional factors parameter(s) provide the independent variable value(s) that correspond to the observed value in *srcWaveName*.

:::note
Cleveland et al. (1992) use the term "multiple factors" instead of "multivariate", hence the keyword name "factors" is used to denote these waves. +
:::

Use one factors wave when srcWaveName is the one-dimensional Y wave of an XY data pair:

```igor
srcWaveName [i] = someFunction(factorWaveName1 [i])
```

Use multiple factors waves when *srcWaveName* contains the values of a multivariate function. "Multivariate" means that *srcWaveName* contains the observed results of a process that combines multiple independent input variables:


```igor
srcWaveName [i] = someFunction(factorWaveName1 [i], factorWaveName2 [i], ... )
```

A maximum of 10 factors waves is supported.

All factors wave(s) must be numeric, noncomplex, one-dimensional and have the same number points as *srcWaveName*.

Any NaN values in *srcWaveName* [i], *factorWaveName1* [i], *factorWaveName2* [i], ... cause all corresponding values to be ignored.

The values in the factors waves may be [NaN](/igorpro/commands/nan.md) only if /DFCT is specified.

Loess does not support NaNs in any of *destFactorWaveName1*, *destFactorWaveName2*... and the results are undefined.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/CONF = {*confInt*, *ciPlusWaveName* [,*ciMinusWaveName*] }</span> |  |
|  | *confInt* specifies the confidence interval (a probability value from 0 to 1). *ciPlusWaveName* and the optional *ciMinusWaveName* are the names of created or overwritten output waves to hold the fitted value +/- the confidence interval. |
|  | <div><Admonition type="note"><p>/CONF uses large memory allocations, approximately N\*N\*8 bytes, where N is the number of points in *srcWaveName* (see **Memory Details**, below).</p></Admonition></div> |
| <span class="table-cell-nowrap">/DEST = *destWaveName*</span> | Specifies the name of the wave to hold the smoothed data. It creates *destWaveName* if it does not already exist or overwrites it if it does. The x (and possibly y) scaling of *destWave* determines the independent (factor) coordinates unless /DFCT={*destFactorWaveName1* [,*destFactorWaveName2*...]} is also specified. |
| <span class="table-cell-nowrap">/DFCT</span> | Specifies that the /DEST wave's x (and possibly y) scaling determines the independent (factor) coordinates at which to compute the smoothed data. |
| <span class="table-cell-nowrap">/DFCT = {*destFactorWaveName1* [,*destFactorWaveName2*...]}</span> |  |
|  | Specifies the names of one-dimensional waves providing the independent coordinates at which to compute the smoothed data. |
|  | If /DFCT={...} is used, the same number of waves must be specified for /DFCT and for factors = {*factorWaveName1* [,*factorWaveName2* ...]}, though their lengths may (and usually will) be different. The length of *destFactorWaveName* waves must be the same as that of the *destWaveName* wave. |
|  | All destination factor waves must be numeric, noncomplex, and one-dimensional. The number of destination factor waves must match the number of source factor waves (if specified), or match the dimensionality of *srcWaveName* (one destination factor wave if *srcWaveName* is one-dimensional, two destination factors waves if *srcWaveName* is two-dimensional.) |
|  | The values in the destination factor waves may not be NaN. |
| <span class="table-cell-nowrap">/E = *extrapolate*</span> | Set *extrapolate* to nonzero to use a slower fitting method that computes values beyond the domain defined by the source factors. This is the "surface" parameter named "direct" in Cleveland et al. (1992). The default is *extrapolate* = 0, which uses the "interpolate" surface parameter, instead. |
| <span class="table-cell-nowrap">/N = *neighbors*</span> | Specifies the number of values in the smoothing window. |
|  | If *neighbors* is even, the next larger odd number is used. When *neighbors* is less than two, no smoothing is done. |
|  | The default is 0.5 * numpnts(*srcWaveName*) rounded up to the next odd integer or 3, whichever is larger. |
|  | Use either /N or /SMTH, not both. |
| <span class="table-cell-nowrap">/NORM[ = *norm* ]</span> | Set *norm* to 0 when specifying multiple factors and they all have the same scale and meaning, for example multiple factors all in units of meters. |
|  | The default is *norm* = 1, which normalizes each factor independently when computing the weighting function. This is appropriate when the factors are not dimensionally related, for example one factor measures wavelength and another measures temperature. |
| <span class="table-cell-nowrap">/ORD = *order*</span> | Specifies the regression (fitting) order, the *d* parameter in Cleveland (1979): |
|  |<table class="nested-table"><tbody><tr><td>*order*&nbsp;=&nbsp;0:</td><td>Fits a constant to the locally-weighted neighbors around each point.</td></tr><tr><td>*order*&nbsp;=&nbsp;1:</td><td>Fits a line to the locally-weighted neighbors around each point (Lowess smoothing).</td></tr><tr><td>*order*&nbsp;=&nbsp;2:</td><td>Default; fits a quadratic (Loess smoothing).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/PASS = *passes*</span> | The number of iterations of local weighting and regression fitting  performed. The minimum is 1 and the default is 4. The *passes* parameter corresponds to the *t* parameter in Cleveland (1979). |
| <span class="table-cell-nowrap">/R[ = *robust* ]</span> | Set *robust* to nonzero to use a robust fitting method that uses a bisquare weight function instead of the normal tricube weight function. This corresponds to the "symmetric" family in Cleveland et al. (1992). The robust method is less affected by outliers. The default is *robust* = 0, which is the "gaussian" family in Cleveland et al. (1992). |
| <span class="table-cell-nowrap">/SMTH = *sf*</span> | another way to express the number of values in the smoothing window,  0 <= *sf* <= 1. The default is 0.5. |
|  | To compute *neighbors* from *sf*, use: |
|  | *neighbors* = 1+floor(*sf* \* numpnts(*srcWaveName*)) |
|  | Use either /N or /SMTH, not both. |
| <span class="table-cell-nowrap">/TIME = *secs*</span> | *secs* is the number of seconds allowed to complete the calculation before either warning (default) or stopping. |
|  | If the stop bit (4) of /V=*verbose* is set, the calculation stops after the alloted time. If the diagnostic bit of /V=*verbose* is also set, warnings about the calculation exceeding the allotted time are printed to the history area. |
|  | As an example, use /TIME=30/V=6 to abort calculations longer than 30 seconds and print the warning to the history area. |
| <span class="table-cell-nowrap">/V[ = *verbose* ]</span> | Controls how much information to print to the history area. *verbose* is a bitwise parameter with each bit controlling one aspect: |
|  |<table class="nested-table"><tbody><tr><td>*verbose*&nbsp;=&nbsp;0:</td><td>No information is printed to the history area (default).</td></tr><tr><td>*verbose*&nbsp;=&nbsp;1:</td><td>Information about the number of observations, equivalent number of parameters, and residual standard error are printed to the history area.</td></tr><tr><td>*verbose*&nbsp;=&nbsp;2:</td><td>Diagnostic information about the number of observations, equivalent number of parameters, and residual standard error are printed to the history area.</td></tr><tr><td>*verbose*&nbsp;=&nbsp;4:</td><td>Use with /TIME. If this bit is set, calculations that exceed *secs* seconds are aborted.</td></tr></tbody></table>
|  | Set *verbose* to 6 to both limit the time and print diagnostic and error messages. |
|  | /V alone is the same as /V=3, which prints both kinds of information. |
|  | S_info contains all the informational messages regardless of the value of *verbose*. |
| <span class="table-cell-nowrap">/Z[ = *z* ]</span> | Set *z* to nonzero to prevent an error from stopping execution. Your procedure can inspect the V_flag variable to see if the smoothing succeeded. |

### *Basic Algorithm* {#basic-algorithm}
The basic locally-weighted regression algorithm fits a constant, line, or quadratic to each point of the source data, using data that falls within the given span of neighbors over the factor data. Data outside of the span is ignored (given a weight of zero), and data inside the span is given a weight that depends on the distance of the data from the point being evaluated: data closer to the point being evaluated have higher weights and have a greater affect on the fit.

The basic algorithm uses the "tricube" weighting function to emphasize near values and deemphasize far values. For the one-factor case (simple XY data), the weighting function can be expressed as:

$$
\displaystyle w_{i}=\left(1-\left|\frac{x-x_{i}}{\max _{q}\left(x-x_{i}\right)}\right|^{3}\right)^{3},
$$

where max<sub>q</sub>(x-x<sub>i</sub>) is the maximum Euclidean distance of the q factor values within the given span from the factor point (x) whose observation (y) value is being evaluated.

The weights are applied to the factor values in the span to compute the constant, linear, or quadratic regression at x.

When multiple factors are used, the Euclidean distance is computed using the one dimension per factor. The default is to normalize each factor's range by the standard deviation of that factor's values before computing the Euclidean distances. When the factors are dimensionally equal, use the /NORM=0 option to skip this normalization.  (See /NORM, about "dimensionally equal".)

### *Robust Algorithm* {#robust-algorithm}
The robust algorithm adds to the basic algorithm a method to identify and remove outliers by rejecting values that exceed a threshold related to the "median absolute deviation" of the basic regression's residuals. The remaining values are used to compute robust "bisquare" weighting values:

$$
r_{i}=\left\{\begin{array}{cc}
\displaystyle \left(1-\left|\frac{e_{i}}{6 \cdot \operatorname{median}\left(\left|e_{i}\right|\right)}\right|^{2}\right)^{2} & \text { for } 0 \leq\left|e_{i}\right|<6 \cdot \operatorname{median}\left(\left|e_{i}\right|\right) \\
0 & \text { for }\left|e_{i}\right|>6 \cdot \operatorname{median}\left(\left|e_{i}\right|\right)
\end{array}\right.
$$

where e<sub>i</sub> is the difference between the observed value and the regression's fitted value, and median( | e<sub>i</sub> | ) is evaluated for all the observed values.

These robust weighting values are multiplied with the original weighting values and a new regression (with new residuals) is computed. This process repeats 4 times by default. Use the /PASS flag to specify a different number of repetitions.

### *Details* {#details}
Loess sets the variable V_flag to 0 if the smoothing was successful, or to an error code if not. Unlike other Igor operations, Loess's /Z flag allows execution to continue even if input parameters are in error.

The information that is printed to the history area when /V is set is always stored in the S_info string, even if /V=0 (which it is by default). S_Info also contains the text of the error message if V_flag is an error code.

The error messages are described in Cleveland et al. (1992). They are often more dire than they seem.

The error message "Span too small. Fewer data values than degrees of freedom" usually means that the /SMTH or /N values are too small. The error code returned in V_Flag for this case is 1106.

The "Extrapolation not allowed with blending" (V_Flag = 1115) error usually means that the destination factors are trying to compute observations outside of the source factors domain without specifying /E=1. This happens if the /DEST *destWaveName* already exists and has X scaling that extends beyond the X scaling of *srcWaveName*. The solution is either kill the /DEST wave, limit the X scaling to the domain of the source wave, or use /E=1.

### *Memory Details* {#memory-details}
Loess requires a lot of memory, especially with the /CONF flag. Even without /CONF, the memory allocations exceed this approximation:

Number of bytes allocated = number of points in *srcWaveName* * 216

With /CONF, Loess can allocate large amounts of memory, approximately N*N*8 bytes, where N is the number of points in *srcWaveName*. The 2GB memory limit of 32-bit addressing limits *srcWaveName* to approximately 10,000 points when using /CONF.

More precisely, the memory allocation may be approximated by this function:


```igor
Function ComputeLoessMemory(srcPoints, numFactorsWaves, doConfidence)
	Variable srcPoints                          // number of points in srcWave, aka N
	Variable numFactorsWaves                    // 1 or number of factors (independent variables)
	Variable doConfidence                       // true if /CONF is specified

	Variable doubles= 9 * srcPoints             // 9 allocated double arrays
	doubles += 5 * numFactorsWaves * srcPoints  // 5 more arrays
	doubles += (1+numFactorsWaves) * srcPoints  // another array
	doubles += (1+numFactorsWaves) * srcPoints  // another array
	doubles += (4+5) * srcPoints                // two more arrays
	if( doConfidence )
		doubles += srcPoints*srcPoints          // one HUGE array
	endif
	Variable bytes= doubles * 8
	return bytes
End

Macro DemoLoessMemory()
	Make/O wSrcPoints={10,100,1000,2000,3000,5000,7500,10000,12500,15000,20000}
	Duplicate/O wSrcPoints, loessMemory, loessMemory3, loessMemoryConf
	SetScale d, 0,0, "Points", wSrcPoints 
	SetScale d, 0,0, "Bytes", loessMemory, loessMemory3, loessMemoryConf 
	loessMemory= ComputeLoessMemory(wSrcPoints[p],1, 0)     // 1 factor (X) no /CONF
	loessMemory3= ComputeLoessMemory(wSrcPoints[p],3, 0)    // 3 factors (X,Y,Z) no /CONF
	loessMemoryConf= ComputeLoessMemory(wSrcPoints[p],1, 1) // 1 factor (X)with /CONF
	Display loessMemory vs wSrcPoints; Append loessMemory3 vs wSrcPoints
	ModifyGraph highTrip(bottom)=1e+08, rgb(loessMemory3)=(0,0,65535)
	ModifyGraph lstyle(loessMemory3)=2
	Legend
	Display loessMemoryConf vs wSrcPoints
	AutoPositionWindow
	ModifyGraph highTrip(bottom)=1e+08
End
```

### *Error Details* {#error-details}

The Loess algorithm fits local polynomials to subsets of data using weighted least squares. Warnings you may receive relate to **evaluation points** and the **local neighborhood** used for fitting. Here's what each concept means:

1. "eval" (Evaluation Points)

	In Loess, the smoothed curve is computed at specific **evaluation points** (`eval`). These are the x-values where the algorithm produces a fitted y-value. `eval` warnings are issued when:

	+ An **evaluation point falls outside the range of the input data** (extrapolation).
	+ The evaluation grid is improperly specified (e.g., zero or negative number of points).

	The algorithm is warning: *"You're asking me to estimate a value at a location where I have little or no supporting data."*

2. "lowerlimit" / "upperlimit"

	These limits define the **bounding box of the predictor data** (the x-range, or in multivariate Loess, the range along each dimension). Warnings involving these arise when:

	+ An **evaluation point is below** `lowerlimit` or **above** `upperlimit` of the original data range. This means the algorithm is being asked to **extrapolate** beyond the observed data, which is unreliable for local regression.
	+ The code is checking: `if (eval[i] < lowerlimit || eval[i] > upperlimit)` and issuing a warning that the fit at that point may be unreliable or degenerate.

	These limits are typically computed as `min(x)` and` max(x)` from the input data. The warning essentially says: *"This evaluation point is outside the convex hull of your data — the result here is an extrapolation and should not be trusted."*

3. "neighborhood radius"

	**This is the core of how Loess works.** For each evaluation point, the algorithm:
	1. Computes the **distance** from the evaluation point to every data point.
	2. Selects the nearest **q** points (where q = `span × n`, with `span` being the smoothing parameter and n the number of data points).
	3. The **neighborhood radius** is the distance to the **farthest** of those q nearest neighbors.
	4. Weights are assigned using a tricube (or similar) kernel function that decays to zero at the neighborhood radius.

	Warnings about **neighborhood radius** occur when:

	+ **The neighborhood radius is zero or near-zero**: This happens when multiple data points coincide at or very near the evaluation point. A zero radius means the weight function can't properly normalize — all selected neighbors are at the same location, so the local regression is degenerate (essentially fitting a constant or has a singular design matrix).
	+ **Too few distinct points in the neighborhood**: If the span is too small, the local polynomial (especially degree 2) may not have enough distinct points to solve the least-squares system, leading to a singular or ill-conditioned matrix.
	+ **The neighborhood doesn't contain enough variation**: Even with enough points, if they all cluster at one x-value, you can't fit a line or parabola through them.

	The typical warning message is something like: *"Neighborhood radius is zero at evaluation point i — the local fit is degenerate."* This is telling the user to **increase the span parameter** so that a wider neighborhood of data points is used, providing enough spread for a meaningful local polynomial fit.

#### *Warnings Summary* {#warnings-summary}

- ***eval***

|  |  |
| --- | --- |
| *Meaning* | The point where the smooth is being calculated |
| *Cause* | Evaluation point outside data range |
| *Fix* | Keep evaluation within data range |

- ***lowerlimit / upperlimit***

|  |  |
| --- | --- |
| *Meaning* | Min/max bounds of input data |
| *Cause* | Extrapolation beyond observed data |
| *Fix* | Don't evaluate outside `[min(x), max(x)]` |

- ***neighborhood radius***

|  |  |
| --- | --- |
| *Meaning* | Distance to farthest neighbor in the local subset |
| *Cause* | Zero radius (coincident points) or too few distinct points |
| *Fix* | Increase `span`; check for duplicate x-values |


### *Examples* {#examples}
You can run these examples by selecting the lines that comprise each example and pressing Control+Enter.

```igor
// 1.  1-D, factors are X scaling, output in new wave
Make/O/N=200 wv=2*sin(x/8)+gnoise(1)
KillWaves/Z smoothed            // ensure Loess creates a new wave
Loess/DEST=smoothed srcWave=wv  // 21-point loess.
Display wv; ModifyGraph mode=3,marker=19
AppendtoGraph smoothed; ModifyGraph rgb(smoothed)=(0,0,65535)

// 2.  1-D, output in existing wave with more points than original data
Make/O/N=100 short=2*cos(x/4)+gnoise(1)
Make/O/N=300 out; SetScale/I x, 0, 99, "" out   // same X range
Loess/DEST=out/DFCT/N=30 srcWave=short
Display short; ModifyGraph mode=3,marker=19
AppendtoGraph out
ModifyGraph rgb(out)=(0,0,65535),mode(out)=2,lsize(out)=2

// 3.  1-D Y vs X wave data interpolated to waveform (Y vs X scaling)
//     with 99% confidence interval outputs
// NOx = f(EquivRatio)
// Y wave
Make/O/D NOx = {4.818, 2.849, 3.275, 4.691, 4.255, 5.064, 2.118, 4.602, 2.286, 0.97, 3.965, 5.344, 3.834, 1.99, 5.199, 5.283, 3.752, 0.537, 1.64, 5.055, 4.937, 1.561};

// X wave (Note that the X wave is not sorted)
Make/O/D EquivRatio = {0.831, 1.045, 1.021, 0.97, 0.825, 0.891, 0.71, 0.801,  1.074, 1.148, 1, 0.928, 0.767, 0.701, 0.807, 0.902,   0.997, 1.224, 1.089, 0.973, 0.98, 0.665};

// Interpolate to dense waveform over X range
Make/O/D/N=100 fittedNOx
WaveStats/Q EquivRatio
SetScale/I x, V_Min, V_max, "", fittedNOx
Loess/CONF={0.99, cp, cm}/DEST=fittedNOx/DFCT/SMTH=(2/3) srcWave=NOx, factors={EquivRatio}
Display NOx vs EquivRatio; ModifyGraph mode=3,marker=19
AppendtoGraph fittedNOx, cp,cm  // fit and confidence intervals
ModifyGraph rgb(fittedNOx)=(0,0,65535)
ModifyGraph mode(fittedNOx)=2,lsize(fittedNOx)=2

// 4.  Interpolate X, Y, Z waves as a 3D surface
Make/O/D vels= {1769, 1711, 1538, 1456, 1608, 1574, 1565, 1692, 1538, 1505}
vels[10] = {1764, 1723, 1540, 1441, 1428, 1584, 1552, 1690, 1673, 1548}
vels[20] = {1485, 1526, 1536, 1591, 1671, 1647, 1608, 1562, 1740, 1753}
vels[30] = {1590, 1466, 1409, 1429}
Make/O/D ews={8.46279, 3.46303, -1.51508, -6.51483, 16.597, -5.95541, -28.5078, 9.68438, -6.00159, -21.7557}
ews[10] = {14.263, 6.02058, -2.25772, -10.536, -18.7785, 10.7509, -6.07024, 1.77531, 0.767701, -0.235545}
ews[20] = {-1.24315, 21.7298, 10.3964, 0.133859, -10.1733, -20.4359, 13.7658, -8.88429, 10.8869, 4.91318}
ews[30] = {-0.0649319, -5.06469, -10.0428, -11.0601}
Make/O/D nss={-38.1732, -15.6207, 6.83407, 29.3865, 3.67947, -1.32028, -6.32004, -10.3852, 6.43591, 23.3302}
nss[10] = {-37.1565, -15.6842, 5.88156, 27.4473, 48.9196, 10.0254, -5.66059, -40.6613, -17.5832, 5.39486}
nss[20] = {28.4729, 43.5833, 20.852, 0.26848, -20.4045, -40.988, 3.0518, -1.9696, -49.1077, -22.1619}
nss[30] = {0.292889, 22.8453, 45.3001, 49.8887}

// Evaluate the smoothed function as interpolated image
Make/O/N=(50,50) velsImage
WaveStats/Q ews
SetScale/I x, V_Min, V_Max, "" velsImage    // destination factors
WaveStats/Q nss
SetScale/I y, V_Min, V_Max, "" velsImage    // are X and Y scaling

Loess/DEST=velsImage/DFCT/NORM=0/SMTH=0.75/E/Z srcWave=vels, factors={ews,nss}

// Display source data as a contour with x, y markers.
Display; AppendXYZContour vels vs {ews,nss}
ModifyContour vels xymarkers=1, labels=0
ColorScale

// Display interpolated surface as an image
AppendImage velsImage
ModifyImage velsImage ctab= {*,*,Grays256,0}
ModifyGraph mirror=2
```

### *References* {#references}
Cleveland, W.S., Robust locally weighted regression and smoothing scatterplots. *J. Am. Stat. Assoc.*, *74*, 829-836, 1979.

Cleveland, W.S., E. Grosse, and M.-J. Shyu, A Package of C and Fortran Routines for Fitting Local Regression Models, Technical Report, Bell Labs, 54pp, 1992.

NIST/SEMATECH, LOESS (aka LOWESS), in *NIST/SEMATECH e-Handbook of Statistical Methods*, [http://www.itl.nist.gov/div898/handbook/pmd/section1/pmd144.htm](http://www.itl.nist.gov/div898/handbook/pmd/section1/pmd144.htm), 2005.

### *See Also* {#see-also}
[Smooth](/igorpro/commands/smooth.md), [Interpolate2](/igorpro/commands/interpolate2.md), [interp](/igorpro/commands/interp.md), [MatrixFilter](/igorpro/commands/matrixfilter.md), [MatrixConvolve](/igorpro/commands/matrixconvolve.md), [ImageInterpolate](/igorpro/commands/imageinterpolate.md)

### *Demos* {#demos}
[Open Loess Demo](#igor-pxp/Examples/Feature__Demos/Loess__Demo.pxp)

[Open Smooth Curve Through Noise Demo](#igor-pxp/Examples/Feature__Demos/Smooth__Curve__Through__Noise.pxp)