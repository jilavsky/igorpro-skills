---
description: "The CurveFit operation fits one of several built-in functions to your data (for user-defined fits, see the FuncFit operation)."
slug: /commands/curvefit
---

<div className="command-signature">

## <strong>CurveFit</strong>  [ <em>flags</em> ] <em>fitType</em>, [<em>kwCWave</em>=<em>coefWaveName</em> ,] <em>waveName</em>  [ <em>flag</em> <em>parameters</em> ] {#curvefit}

</div>

The CurveFit operation fits one of several built-in functions to your data (for user-defined fits, see the [FuncFit](/igorpro/commands/funcfit.md) operation). When fitting with CurveFit and built-in fit functions, automatic initial guesses will provide a good starting point in most cases.

The results of the fit are returned in a wave, by default W_coef. In addition, the results are put into the system variables K0, K1 ... K*n* but the use of the system variables is limited and considered obsolete.

As explained under [Fitting with Complex-Valued Functions](/igorpro/analysis/curve-fitting.md#fitting-with-complex-valued-functions), a user-defined fitting function can return complex values. A complex fitting function can be written to require a complex coefficient wave in which case the system variables are not supported.

You can specify your own wave for the coefficient wave instead of W_coef using the kwCWave keyword.

Virtually all waves specified to the CurveFit operation can be a sub-range of a larger wave using the same sub-range syntax as the Display operation uses for graphing. See ***Wave Subrange Details*** below.

See [Curve Fitting](/igorpro/analysis/curve-fitting.md) for detailed information including the use of the Curve Fit dialog.

CurveFit operation parameters are grouped in the following categories: flags, fit type, parameters (kwCWave=*coefWaveName* and *waveName*), and flag parameters. The sections below correspond to these categories. Note that flags must precede the fit type and flag parameters must follow *waveName*.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B = *pointsPerCycle*</span> | Used when *type* is sin; *pointsPerCycle* is the estimated number of data points per sine wave cycle. This helps provide initial guesses for the fit. You may need to try a few different values on either side of your estimated points/cycle. |
| <span class="table-cell-nowrap">/C</span> | Make constraint matrix and vector. This only applies if you use the /C=*constraintSpec* parameter to specify constraints (see above). A matrix called M_FitConstraint and a vector called W_FitConstraint are created. For more information, see [Fitting with Constraints](/igorpro/analysis/curve-fitting.md#fitting-with-constraints). |
| <span class="table-cell-nowrap">/G</span> | Use values in variables K0, K1... K*n* as starting guesses for a fit. If you specify a coefficient wave with the kwCWave keyword, the starting guesses will be read from the coefficient wave. |
| <span class="table-cell-nowrap">/H = "*hhh...*"</span> | Specifies coefficients to hold constant. |
|  | *h* is 1 for coefficients to hold, 0 for coefficients vary. |
|  | E.g., /H="100" holds K0 constant, varies K1 and K2. |
| <span class="table-cell-nowrap">/K = {*constants* }</span> | Sets values of constants (not fit coefficients) in certain fitting functions. For instance, the exp_XOffset function contains an X offset constant. Built-in functions will set the constant automatically, but the automatic value can be overridden using this flag. |
|  | *constants* is a list of constant values, e.g., /K={1,2,3}. The length of the list must match the number of constants used by the chosen fit function. |
|  | This flag is not currently supported by the Curve Fit dialog. Use the To Cmd button and add the flag on the command line. |
| <span class="table-cell-nowrap">/L = *destLen*</span> | Sets the length of the wave created by the AutoTrace feature, that is, /D without destination wave (see the /D parameter below, in the section *Flag Parameters*). The length of the wave fit_*waveName* will be set to *destLen*. This keyword also sets the lengths of waves created for confidence and prediction bands. |
| <span class="table-cell-nowrap">/M = *doMat*</span> | Generate the covariance matrix. If *doMat* =2, the covariance matrix is put into a 2D matrix wave called M_Covar. If *doMat* =1 or is missing, the covariance matrix is generated as the 1D waves CM_K*n*, where *n* is from 0 (for K0) to the number of coefficients minus one. If *doMat* =0, the covariance matrix is not generated. *doMat* =1 is included for compatibility with previous versions of Igor; it is better to use *doMat* =2. |
|  | CurveFit does not generate the covariance matrix for line fits. Instead it reports the coefficient of correlation via the output variable V_rab. |
| <span class="table-cell-nowrap">/N[ = *updateMode* ]</span> | Controls updating of windows during a curve fitting operation. Updating windows after each iteration can slow curve fitting down significantly. |
|  |<table class="nested-table"><tbody><tr><td>*updateMode*&nbsp;=&nbsp;0:</td><td>An update is done every iteration so that you can monitor the progress of a fit. An update is performed when the fit finishes.</td></tr><tr><td>*updateMode*&nbsp;=&nbsp;1:</td><td>Suppresses updates after each fit iteration. If you use the /X flag, a screen update is done to ensure that the X range is accurate. /N is the same as /N=1. This is the default update mode.</td></tr><tr><td>*updateMode*&nbsp;=&nbsp;2:</td><td>Suppresses all updates including when using the /X flag. In a user-defined function, you must ensure that your graph has been updated by calling [DoUpdate](/igorpro/commands/doupdate.md) if you use the /X flag. This mode requires Igor Pro 9.00 or later.</td></tr></tbody></table>
|  | See ***Curve Fitting Screen Updates*** below for details. |
| <span class="table-cell-nowrap">/NTHR = *nthreads*</span> | This flag is accepted but is obsolete and does nothing. See [Curve Fitting with Multiple Processors](/igorpro/analysis/curve-fitting.md#curve-fitting-with-multiple-processors) for further information. |
| <span class="table-cell-nowrap">/O</span> | Only generate initial guesses; doesn't actually do the fit. |
|  | Unless /ODR=2, this flag is ignored when used with linear fit types (line, poly, poly_XOffset and poly2D). The [FuncFit](/igorpro/commands/funcfit.md) operation also ignores this flag. |
| <span class="table-cell-nowrap">/ODR = *fitMethod*</span> | Selects a method for fitting. The possibilities are: |
|  |<table class="nested-table"><tbody><tr><td>*fitMethod*&nbsp;=0:</td><td>Default. Levenberg-Marquardt least-squares method using old code.</td></tr><tr><td>*fitMethod*&nbsp;=1:</td><td>Trust-region Levenberg-Marquardt ordinary least-squares method implemented using ODRPACK95 code. See [Curve Fitting References](/igorpro/analysis/curve-fitting.md#curve-fitting-references).</td></tr><tr><td>*fitMethod*&nbsp;=2:</td><td>Trust-region Levenberg-Marquardt least orthogonal distance method implemented using ODRPACK95 code. This method is appropriate for fitting when there are measurement errors in the independent variables, sometimes called &quot;errors in variables fitting&quot;, &quot;random regressor models,&quot; or &quot;measurement error models&quot;.</td></tr><tr><td>*fitMethod*&nbsp;=3:</td><td>Implicit fit. No dependent variable is specified; instead fitting attempts to adjust the fit coefficients such that the fit function returns zero for all dependent variables.</td></tr><tr><td></td><td>Implicit fitting will be of almost no use with the built-in fitting functions. Instead, use [FuncFit](/igorpro/commands/funcfit.md) and a user-defined fit function designed for an implicit fit.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Q[ = *quiet* ]</span> | If *quiet* = 1, prevents results from being printed in history. /Q is the same as /Q=1. |
| <span class="table-cell-nowrap">/TBOX = *textboxSpec*</span> | If the top graph displays the fitted data, the /TBOX flag adds an annotation to the graph or updates the annotation if it already exists. Graphs other than the top graph are not affected. |
|  | The textbox contains a customizable set of information about the fit. The *textboxSpec* parameter is a bitfield to select various elements to be included in the textbox: |
|  |<table class="nested-table"><tbody><tr><td>**textboxSpec**</td><td>**Selects This Element**</td></tr><tr><td>1</td><td>Title &quot;Curve Fit Results&quot;</td></tr><tr><td>2</td><td>Date</td></tr><tr><td>4</td><td>Time</td></tr><tr><td>8</td><td>Fit Type (Least Squares, ODR, etc.)</td></tr><tr><td>16</td><td>Fit function name</td></tr><tr><td>32</td><td>Model Wave, the autodestination wave (includes a symbol for the trace if appropriate)</td></tr><tr><td>64</td><td>Y Wave, with trace symbol</td></tr><tr><td>128</td><td>X Wave</td></tr><tr><td>256</td><td>Coefficient value report</td></tr><tr><td>512</td><td>Include errors in the coefficient value report</td></tr></tbody></table>
|  | Request inclusion of various parts by adding up the values for each part you want. |
|  | *textboxSpec* defaults to all bits on. |
|  | Setting *textboxSpec* to zero removes the textbox. |
| <span class="table-cell-nowrap">/W = *wait*</span> | Specifies behavior for the curve fit results window. |
|  |<table class="nested-table"><tbody><tr><td>*wait*&nbsp;=1</td><td>Wait till user clicks OK button before dismissing curve fit results window. This is the default behavior from the command line or dialog.</td></tr><tr><td>*wait*&nbsp;=0</td><td>Display the curve fit results window but do not wait for the user to click the OK button.</td></tr><tr><td>*wait*&nbsp;=2</td><td>Do not display the curve fit results window at all. This is the default for fits run from a procedure.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/X [ = *fullRange*]</span> | /X or /X=1 sets the X scaling of the auto-trace destination wave to match the appropriate X axis on the graph when the Y data wave is on the top graph. This is useful when you want to extrapolate the curve outside the range of  X data being fit. |
|  | If you omit /X or specify /X=0, the X scaling of the auto-trace destination wave is set to match the range of X values being fit. |

### *Fit Types* {#fit-types}
*fitType* is one of the built-in curve fit function types:


|  |  |
| --- | --- |
| gauss | Gaussian peak: y = K0+K1\*exp(-((x-K2)/K3)^2). |
| lor | Lorentzian peak: y = K0+K1/((x-K2)^2+K3). |
| Voigt | Fits a Voigt peak, a convolution of a Lorentzian and a Gaussian peak. By changing the ratio of the widths of the Lorentzian and Gaussian peak components the shape can grade between a Lorentzian shape and a Gaussian shape: |
|  | y = [VoigtPeak](/igorpro/commands/voigtpeak.md)(W_coef, x) |
| exp_XOffset | Exponential:  y = K0+K1\*exp(-(x-x0)/K2). |
|  | x0 is a constant; by default it is set to the minimum X value involved in the fit. Inclusion of x0 prevents problems with floating-point roundoff errors that can afflict the exp function. |
| dblexp_XOffset | Double exponential: |
|  | y = K0+K1\*exp(-(x-x0)/K2)+K3\*exp(-(x-x0)/K4) |
|  | x0 is a constant; by default it is set to the minimum X value involved in the fit. Inclusion of x0 prevents problems with floating-point roundoff errors that can afflict the exp function. |
| exp | Exponential: y = K0+K1\*exp(-K2*x). |
| dblexp | Double exponential: y = K0+K1\*exp(-K2\*x)+K3\*exp(-K4\*x). |
| dblexp_peak | Double exponential with amplitudes of opposite sign, making a peak: |
|  | y = K0+K1\*(exp(-(x-K4)/K2)+exp(-(x-K4)/K3)). |
| sin | Sinusoid: y = K0+K1\*sin(K2\*x+K3). |
| line | Line: y = K0+K1\*x. |
| poly *n* | Polynomial: y = K0+K1\*x+K2\*x^2+... |
|  | *n* must be greater than zero. *n* is the number of terms or the degree plus one. Prior to Igor Pro 9.00, the minimum accepted value for *n* was 3.<br>There is no upper limit to *n*, but we recommend moderation. Floating-point truncation errors impose a poorly-defined practical limit. If you fit high-degree polynomials, be sure the X range is near the [-1, 1] range, or use the poly_XOffset fit type. |
|  | *n* = 1 is equivalent to finding the mean of the Y values, and *n* = 2 fits a line to the data set, but doesn't output the special statistical information you get if you use the *line* fit type. |
| poly_XOffset *n* | Polynomial: y = K0+K1\*(x-x0)+K2\*(x-x0)^2+... |
|  | *n* must be greater than zero. *n* is the number of terms or the degree plus one. Prior to Igor Pro 9.00, the minimum accepted value for *n* was 3. |
|  | *n* = 1 is equivalent to finding the mean of the Y values, and *n* = 2 fits a line to the data set, but doesn't output the special statistical information you get if you use the *line* fit type.<br>There is no upper limit to *n*, but we recommend moderation. While the poly_XOffset fit type is better than the poly fit type, floating-point truncation errors impose a poorly-defined practical limit. |
|  | x0 is a constant; by default it is set to the minimum X value involved in the fit. Inclusion of x0 prevents problems with floating-point roundoff errors when the X values in your fit are far from the origin. Note that even so, high-degree polynomials may be problematic.. |
| hillequation | Hill's Equation: K0+(K1-K0)\*(x^K2/(1+(x^K2+K3^K2))) |
|  | This is a sigmoidal function. X values must be greater than 0. |
| sigmoid | y = K0+K1/(1+exp(-(x-K2)/K3)). |
| power | Power law: K0+K1\*x^K2. X values must be greater than 0. |
| lognormal | Log normal: K0+K1\*exp(-(ln(x/K2)/K3)^2). X values must be greater than 0. |
| log | Log base 10: K0+K1\*log(x). X values must be greater than 0. |
|  | Log was added in Igor Pro 9.00. |
| gauss2D | Two-dimensional gaussian: |
|  | K0+K1\*exp((-1/(2\*(1-K6^2)))\*(((x-K2)/K3)^2 + ((y-K4)/K5)^2 - (2\*\K6\*\(x-K2)\*(y-K4)/(K3\*K5)))) |
|  | The cross-correlation coefficient (K6) must be between -1 and 1. This coefficient is automatically constrained to lie in that range. If you are confident that the correlation is zero, it may greatly speed the fit to hold it at zero. |
| poly2D *n* | Two-dimensional polynomial: K0+K1\*x+K2\*y+K3\*x^2+K4\*xy+K5\*y^2+... |
|  | *n* is the degree of the polynomial. All terms up to degree *n* are included, including cross terms. For instance, degree 3 terms are x<sup>3</sup>, x<sup>2</sup>y, xy<sup>2</sup> and y<sup>3</sup>. |

For more details on the built-in fit functions, see [Built-in Curve Fitting Functions](/igorpro/analysis/curve-fitting.md#built-in-curve-fitting-functions).

### *Parameters* {#parameters}
kwCWave=*coefWaveName* specifies an optional coefficient wave. If present, the specified coefficient wave is set to the final coefficients determined by the curve fit. If absent, a wave named W_coef is created and is set to the final coefficients determined by the curve fit.

If you use kwCWave=*coefWaveName* and you include the /G flag, initial guesses are taken from the specified coefficient wave.

*waveName* is the wave containing the dependent variable data to be fit to the selected function *type*. For functions of just one independent variable, the dependent variable data is often referred to as "Y data". You can fit to a subrange of the wave by supplying (*startX*,*endX* ) after the wave name. Though not shown in the syntax description, you can also specify the subrange in points by supplying [*startP*,*endP* ] after the wave name. See ***Wave Subrange Details***, below, for more information on subranges of waves in curve fitting.

If you are using one of the two-dimensional fit functions (gauss2D or poly2D) either *waveName* must name a matrix wave or you must supply a list of X waves via the /X flag.

### *Flag Parameters* {#flag-parameters}

These flag parameters must follow waveName.

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = appendResid</span> | appendResid =1 to allow the automatically-generated residual to be appended to the graph, appendResid =0 to prevent appending. With appendResid =0, the wave is generated and filled with residual values, but not appended to the graph. The default is /A=1. |
| <span class="table-cell-nowrap">/AD[ = *doAutoDest ]*</span> | If *doAutoDest* is 1, it is the same as /D alone. /AD is the same as /AD=1. |
| <span class="table-cell-nowrap">/AR = *doAutoResid*</span> | If *doAutoResid* is 1, it is the same as /R alone. /AR is the same as /AR=1. |
| <span class="table-cell-nowrap">/C = *constraintSpec*</span> | Apply linear constraints during curve fitting. Constraints can be in the form of a text wave containing constraint expressions (/C=*textWaveName* ) or a suitable matrix and vector (/C={*constraintMatrix*, *constraintVector*}). See [Fitting with Constraints](/igorpro/analysis/curve-fitting.md#fitting-with-constraints) for details. |
|  | <div><Admonition type="note"><p>Constraints are not available for the built-in line, poly and poly2D fit functions. To apply constraints to these fit functions you must create a user-defined fit function.</p></Admonition></div> |
| <span class="table-cell-nowrap">/D[ = *destwaveName* ]</span> | *destwaveName* is evaluated based on the equation resulting from the fit. *destwaveName* must have the same length as *waveName.* |
|  | If only /D is specified, an automatically-named wave is created. The name is based on the *waveName* with "fit_" as a prefix. This automatically named wave will be appended (if necessary) to the top graph if *waveName* is graphed there. The X scaling of the automatically named wave is set from the range of x data used during the fit. |
|  | By default the length of the automatically-created wave is 200 points (or 2 points for a straight line fit). This can be changed with the /L flag. |
|  | If *waveName* is a 1D wave displayed on a logarithmic X axis, Igor also creates an X wave with values exponentially spaced. The name is based on *waveName* with "fitX_" as a prefix. |
|  | If you fit to a user-defined function that returns complex values, the destination wave will also be complex. |
| <span class="table-cell-nowrap">/F = {*confLevel*, *confType* [, *confStyleKey* [, *waveName ...*]]}</span> |  |
|  | Calculate confidence intervals for a confidence level of *confLevel*. The value of confLevel must be between 0 and 1 corresponding to confidence levels of 0 to 100 per cent. |
|  | *confType* selects what to calculate: |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Confidence bands for the model</td></tr><tr><td>2:</td><td>Prediction bands for the model</td></tr><tr><td>4:</td><td>Confidence intervals for the fit coefficients</td></tr></tbody></table>
|  | These values can be added together to select multiple options. That is, to select both a confidence band and fit coefficient confidence intervals, set *confType* to 5. |
|  | Confidence and prediction bands can be shown as waves contouring the specified confidence level (use "Contour" for *confStyleKey*) or as error bars (use "ErrorBar" for *confStyleKey*). The default is Contour. |
|  | If no waves are specified, waves to contain the results are automatically generated and appended to the top graph (if the top graph contains the fitted data). See below for details on the waves for confidence bands. |
|  | <div><Admonition type="note"><p>Confidence bands and prediction bands are not available for multivariate curve fits.</p></Admonition></div> |
| <span class="table-cell-nowrap">/I[ = *weightType* ]</span> | If *weightType* is 1, the weighting wave (see /W parameter below) contains standard deviations. If *weightType* is 0, the weighting wave contains reciprocal of the standard deviation. If the /I parameter is not present, the default is /I=0. |
| <span class="table-cell-nowrap">/M = *maskWaveName*</span> | Specifies that you want to use the wave named *maskWaveName* to select points to be fit. The mask wave must match the dependent variable wave in number of points and dimensions. Setting a point in the mask wave to zero or NaN (blank in a table) eliminates that point from the fit. The mask wave must be real even when fitting complex data. |
| <span class="table-cell-nowrap">/R[ = *residwaveName* ]</span> | The elements of *residwaveName* are calculated by subtracting model values from the data values. *residwaveName* must have the same length as *waveName.* |
|  | If only /R is specified, an automatically-named wave is created with the same number of points as *waveName*. The name is based on *waveName* with "Res_" as a prefix. If a new wave needs to be created, it is automatically filled with NaN, but if the wave already exists it is simply re-used. |
|  | During fitting the residual is computed only for points that actually participate in the fit. If you fit to a subrange or use a mask wave to fit to specific points, only those points are stored. See [Residuals Using Auto Trace](/igorpro/analysis/curve-fitting.md#residuals-using-auto-trace) for details. |
|  | The automatically created residual wave is appended (if necessary) to the top graph if *waveName* is graphed there. The residual wave is appended to a new free axis named by prepending "Res_" to the name of the vertical axis used for plotting the Y data. To the extent possible, the new free axis is formatted nicely. |
|  | If the graph containing the data to be fit has very complex formatting, you may not wish to have the residual automatically appended to the graph. In this case, use /A=0, as documented above. |
|  | If you fit to a user-defined function that returns complex values, the residual wave will also be complex. |
| <span class="table-cell-nowrap">/W = *wghtwaveName*</span> | *wghtwaveName* contains weighting values applied during the fit, and must have the same length as *waveName*. These weighting values can be either the reciprocal of the standard errors, or the standard errors. See the /I parameter above for details. |
|  | If you fit to a user-defined function that returns complex values, the weighting wave must also be complex. |
| <span class="table-cell-nowrap">/X = *xwaveName*</span> | The X values for the data to fit come from *xwaveName*, which must have the same length as *waveName.* |
|  | If you are fitting to one of the two-dimensional fit functions and *waveName* is a matrix wave, *xwaveName* supplies independent variable data for the X dimension. In this case, *xwaveName* must name a 1D wave with the same number of rows as *waveName*. |
|  | When fitting to a complex-valued fit function, the X waves must be real or complex consistent with the X input or parameters declared by your fitting function. |
| <span class="table-cell-nowrap">/X = {*xwave1*, *xwave2* }</span> | For fitting to one of the two-dimensional fit functions when *waveName* is a 1D wave. *xwave1* and *xwave2* must have the same length as *waveName*. |
| <span class="table-cell-nowrap">/Y = *ywaveName*</span> | For fitting using one of the 2D fit functions if *waveName* is a matrix wave. *ywaveName* must be a 1D wave with length equal to the number of columns in *waveName*. |
| <span class="table-cell-nowrap">/NWOK</span> | Allowed in user-defined functions only. When present, certain waves may be set to null wave references. Passing a null wave reference to CurveFit is normally treated as an error. By using /NWOK, you are telling CurveFit that a null wave reference is not an error but rather signifies that the corresponding flag should be ignored. This makes it easier to write function code that calls CurveFit with optional waves. |
|  | The waves affected are the X wave or waves (/X), weight wave (/W), mask wave (/M) and constraint text wave (/C). The destination wave (/D=wave) and residual wave (/R=wave) are also affected, but the situation is more complicated because of the dual use of /D and /R to mean "do autodestination" and "do autoresidual". See /AR and /AD. |
|  | If you don't need the choice, it is better not to include this flag, as it disables useful error messages when a mistake or run-time situation causes a wave to be missing unexpectedly. |
|  | <div><Admonition type="note"><p>To work properly this flag must be the last one in the command.</p></Admonition></div> |

### *Flag Parameters for Nonzero /ODR* {#flag-parameters-for-nonzero-odr}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/XW = *xWeightWave*</span> |  |
| <span class="table-cell-nowrap">/XW = {*xWeight1*, *xWeight2* }</span> |  |
|  | /ODR=2 or 3 only. |
|  | *xWeightWave* contains weighting values for the independent variables, and must have the same length as *waveName*. When fitting to one of the multivariate fit functions such as poly2D or Gauss2D, you must supply a weight wave for each independent variable using the second form. |
|  | Weighting values can be either the reciprocal of the standard errors, or the standard errors. The choice of standard error or reciprocal standard error must be the same for both /W and /XW. See the /I flag above for details. |
|  | When fitting to a complex-valued fit function, the X weighting waves must be real or complex consistent with the X parameters declared by your fitting function. |
| <span class="table-cell-nowrap">/XHLD = *holdWave*</span> |  |
| <span class="table-cell-nowrap">/XHLD = {*holdWave1*, *holdWave2* }</span> |  |
|  | /ODR=2 or 3 only. |
|  | A wave or waves to hold the values of the independent variables fixed during orthogonal distance regression. The waves must match the input X data; a one in a wave element fixes the value of the corresponding X value. |
| <span class="table-cell-nowrap">/CMAG = *scaleWave*</span> | Nonzero /ODR only. Specifies a wave that indicates the expected scale of the fit coefficients at the solution. If different coefficients have very different orders of magnitude of expected values, this can improve the efficiency and accuracy of the fit. |
| <span class="table-cell-nowrap">/XD = *xDestWave*</span> |  |
| <span class="table-cell-nowrap">/XD = {*xDestWave1*, *xDestWave2* }</span> |  |
|  | /ODR=2 or 3 only. |
|  | Specifies a wave or waves to receive the fitted values of the independent variables during a least orthogonal distance regression. |
|  | When fitting to a complex-valued fit function, the X destination waves must be real or complex consistent with the X parameters declared by your fitting function. |
| <span class="table-cell-nowrap">/XR = *xResidWave*</span> |  |
| <span class="table-cell-nowrap">/XR = {*xResidWave1*, *xResidWave2* }</span> |  |
|  | /ODR=2 or 3 only. |
|  | Specifies a wave or waves to receive the differences between fitted values of the independent variables and the starting values during a least orthogonal distance regression. That is, they will be filled with the X residuals. |
|  | When fitting to a complex-valued fit function, the X residual waves must be real or complex consistent with the X parameters declared by your fitting function. |
| <span class="table-cell-nowrap">/PNLT = *penalty*</span> | /ODR=3 only. Sets the starting value of the penalty parameter for implicit ODR fits. If *penalty* is less than or equal to zero, the ODRPACK default value is used. The penalty parameter controls the balance between minimizing the sum of squared residuals and satisfying the implicit equation. You normally do not need to set this; the default works well in most cases. |
|  | <div><Admonition type="caution"><p>This flag is for advanced users only. Changing the penalty parameter can cause convergence failures if set incorrectly.</p></Admonition></div> |
| <span class="table-cell-nowrap">/ODRT = {*chiSqTol*, *paramTol*}</span> | For nonzero /ODR. Sets convergence tolerances for ODR fitting. *chiSqTol* is the relative convergence tolerance for the sum of squared residuals. *paramTol* is the relative convergence tolerance for the fit parameters. If either value is less than or equal to zero, the ODRPACK default is used (sqrt(machine epsilon) for *chiSqTol*, (machine epsilon)^(2/3) for *paramTol*). You normally do not need to set these unless you need tighter or looser convergence criteria than the defaults. |
|  | <div><Admonition type="caution"><p>This flag is for advanced users only. Setting tolerances too tight can prevent convergence; setting them too loose can produce inaccurate results.</p></Admonition></div> |

### *Details* {#details}
CurveFit gets initial guesses from the Kn system variables when user guesses (/G) are specified, unless a coefficient wave is specified using the kwCWave keyword. Final curve fit parameters are written into a wave name W_coef, unless you specify a coefficient wave with the kwCWave keyword.

For compatibility with earlier versions of Igor, the parameters are also stored in the system variables Kn. This can be a source of confusion. We suggest you think of W_coef as the output coefficients and Kn as ***input*** coefficients that get overwritten.

Other output waves are M_Covar (see the /M flag), M_FitConstraint and W_FitConstraint (see /C parameter and [Fitting with Constraints](/igorpro/analysis/curve-fitting.md#fitting-with-constraints)), W_sigma. If you have selected coefficient confidence limits using the /F parameter, a wave called W_ParamConfidenceInterval is created with the confidence intervals for the fit coefficients.

CurveFit stores other curve fitting statistics in variables whose names begin with "V_". CurveFit also looks for certain V_ variables which you can use to modify its behavior. See [Curve Fitting](/igorpro/analysis/curve-fitting.md) and [Special Variables for Curve Fitting](/igorpro/analysis/curve-fitting.md#special-variables-for-curve-fitting) for details.

When fitting with /ODR=nonzero, fitting with constraints is limited to simple "bound constraints". That is, you can constrain a fit coefficient to be greater than or less than some value. Constraints involving combinations of fit coefficients are supported only with /ODR=0. The constraints are entered in the same way, using an expression like "K0 > 1".

### *Wave Subrange Details* {#wave-subrange-details}
Almost any wave you specify to CurveFit can be a subrange of a wave. The syntax for wave subranges is the same as for the Display command; see [Subrange Display Syntax](/igorpro/graphing/graphs.md#subrange-display-syntax) for details. However, the Display command allows only one dimension to have a range (multiple elements from the dimension); if a multidimensional wave is appropriate for CurveFit, you may use a range for more than one dimension.

Some waves  must have the same number of points as other waves. For instance, a one-dimensional Y wave must have the same number of points as any X waves. Thus, if you use a subrange for an X wave, the number of points in the subrange must match the number of points being used in the Y wave (but see the following subsection, ***Subrange Backward Compatibility*** for a complication to this rule).

A common use of wave subranges might be to package all your data into a single multicolumn wave, along with the residuals and model values. For a univariate fit, you might need X and Y waves, plus a destination (model) wave and a residual wave. You can achieve all of that using a 4 column wave. For example:


```igor
Make/D/N=(100, 4) Data
... fill column zero with X data and column one with Y data ...
CurveFit poly 3, Data[][1] /X=Data[][0]/D=Data[][2]/R=Data[][3]
```

Note that because all the waves are full columns from a single multicolumn wave, the number of points is guaranteed to be the same.

The number of points used for X waves (*xwaveName* or {*xwave1, xwave2, ...*}), weighting wave (*wghtwaveName*), mask wave (*maskWaveName*), destination wave (*destwaveName*) and residual wave (*residwaveName*) must be the same as the number of points used for the Y wave (*waveName*). If you specify your own confidence band waves (/F flag) they must match the Y wave; you cannot use subranges with confidence band waves. If you set /ODR = nonzero, the X weight, hold, destination and residuals waves must match the Y wave.

The total number of points in each wave does not need to match other waves, just the number of points in the specified subrange.

When fitting to a univariate fit function (that includes almost all the fit types) the Y wave must have effectively one dimension. That means the Y wave must either be a 1D wave, or it must have a subrange that makes the data being used one dimensional. For instance:


```igor
Make/N=(100,100) Ydata      // 2D wave
CurveFit gauss Ydata[][0]   // OK- a single column is one-dimensional
CurveFit gauss Ydata[2][]   // OK- s single row is one-dimensional
CurveFit gauss Ydata        // not OK- Ydata is two-dimensional
CurveFit gauss Ydata[][0,1] // not OK- two columns makes 2D subrange
```

When fitting a multivariate function ([poly2D](/igorpro/commands/poly2d.md) or [Gauss2D](/igorpro/commands/gauss2d.md)) you have the choice of making the Y data either one-dimensional or two-dimensional. If it is one-dimensional, then you must be fitting XYZ (or Y,X1,X2) triplets. In that case, you must provide a one-dimensional Y wave and two one-dimensional X waves, or 2 columns from a multicolumn wave. For instance:

These are OK:


```igor
Make/N=(100,3) myData
CurveFit Gauss2D myData[][0] /X={myData[][1],myData[][2]}
CurveFit Gauss2D myData[][0] /X=myData[][1,2]
```

These are not OK:


```igor
// 2D Y wave with 1D X waves
CurveFit Gauss2D myData /X={myData[][1],myData[][2]}
// too many X columns
CurveFit Gauss2D myData[][0] /X=myData
```

If you use a 2D Y wave, the X1 and X2 data can come from the grid positions and the Y wave's X and Y index scaling, or you can use one-dimensional waves or wave subranges to specify the X1 and X2 positions of the grid:


```igor
Make/N=(20,30) yData
CurveFit Gauss2D yData	//OK- 2D Y data, X1 and X2 from scaling
Make/N=20 x1Data
Make/N=30 x2Data
// OK: 2D effective Y data, matching 1D X and Y flags
CurveFit Gauss2D yData[0,9][0,19] /X=x1Data[0,9]/Y=x2data[10,29]
// OK: effective 2D Y data
Make/N=(10,20,3) Y data
CurveFit Gauss2D yData[][][0]
```

There are, of course, lots of possible combinations, too numerous to enumerate.

### *Subrange Backward Compatibility* {#subrange-backward-compatibility}
Historically, a Y wave could have a subrange. The same subrange applied to all other waves. For backward compatibility, if you use a subrange with the Y wave only, and other waves lack a subrange, these other waves must have either: 1) The same total number of points as the total number of points in the Y wave in which case the Y wave subrange will be applied; or 2) The same total number of points as the Y wave's subrange.

In addition, the Y wave can take a subrange in parentheses to indicate that the subrange refers to the Y wave's scaled indices (X scaling). If you use parentheses to specify an X range, you must satisfy the old subrange rules: All waves must have the same number of points. Subrange is allowed for the Y wave only. The Y wave subrange is applied to all other waves.

### *Confidence Band Details* {#confidence-band-details}
Automatic generation of confidence and prediction bands occurs if the /F={...} parameter is used with no wave names. One to four waves are generated, or you can specify one to four wave names yourself depending on the *confKind* and *confStyle* settings

Waves auto-generated by /F={*confLevel*, *confKind*, *confStyle* }:

| confKind | confStyle | What You Get | Auto Wave Names |
| --- | --- | --- | --- |
| 1 | "Contour" | upper and lower | UC_*dataName* |
|  |  | confidence contours | LC_*dataName* |
| 2 | "Contour" | upper and lower | UP_*dataName* |
|  |  | prediction contours | LP_*dataName* |
| 3 | "Contour" | upper and lower | UC_*dataName* |
|  |  | confidence contours | LC_*dataName* |
|  |  | and prediction | UP_*dataName* |
|  |  | contours | LP_*dataName* |
| 1 | "ErrorBar" | confidence interval | CI_*dataName* |
|  |  | wave |  |
| 2 | "ErrorBar" | prediction interval | PI_*dataName* |
|  |  | wave |  |
| 3 | "ErrorBar" | confidence and | CI_*dataName* |
|  |  | prediction interval | PI_*dataName* |
|  |  | waves |  |

Note that *confKind* may have 4 added to it if you want coefficient confidence limits calculated as well.

The contour waves are appended to the top graph as traces if the data wave is displayed in the top graph. The wave names have *dataName* replaced with the name of the wave containing the Y data for the fit.

Waves you must supply for /F={*confLevel*, *confKind*, *confStyle*, *wave*, *wave...*}:

| confKind | confStyle | You Supply |
| --- | --- | --- |
| 1 | "Contour" | 2 waves to receive upper and lower confidence contours |
| 2 | "Contour" | 2 waves to receive upper and lower prediction contours |
| 3 | "Contour" | 4 waves to receive upper and lower confidence and upper and lower prediction contours |
| 1 | "ErrorBar" | 1 wave to receive values of confidence band width |
| 2 | "ErrorBar" | 1 wave to receive values of prediction band width |
| 3 | "ErrorBar" | 2 waves to receive values of confidence and prediction band widths |

The waves you supply must have the same number of points as the dependent variable data wave. The band intervals will be calculated at the X values of the input data. These waves are not automatically appended to a graph; it is expected that you will display the contour waves as traces or use the error bar waves to make error bars on the model fit wave.

### *Residual Details* {#residual-details}
Residuals are calculated only for elements corresponding to elements of *waveName* that are included in the fit. Thus, you can calculate residuals automatically for a piecewise fit done in several steps.

The automatic residual wave will be appended to the top graph if the graph displays the Y data. It is appended to a new free axis positioned directly above the axis used to display the Y data, making a stacked graph. Other axes are shortened as necessary to make room for the new axis. You can alter the axis formatting afterwards. See [Creating Stacked Plots](/igorpro/graphing/graphs.md#creating-stacked-plots).

While Igor will go to some lengths to make a nicely formatted stacked graph, the changes made to the graph formatting may be undesirable in certain cases. Use /A=0 to suppress the automatic append to the graph. The automatic residual wave will be created and filled with residual values, but not appended to the graph.

### *Curve Fitting Screen Updates* {#curve-fitting-screen-updates}
A screen update redraws windows displaying data that has changed since the previous update, if any. Updates can take a significant amount of time, so the /N flag allows you to control them during a curve fitting operation.

Igor historically performed a screen update after each curve fitting iteration so that a graph showing the fit destination would display the latest trial solution after each iteration. This was default behavior, equivalent to /N=0.

As processors became faster, updating after every iteration became less useful because,  in most cases, the time between iterations is short and the entire fit finishes quickly. Consequently, for Igor Pro 7.00, we changed the default to update only at the end of a fit, equivalent to /N=1.

There are some potential pitfalls to suppressing screen updates.

If you use the /X flag to tell Igor to extrapolate the fit curve to the entire X range of a graph, and if your procedures alter the X axis range, you need to call DoUpdate before calling CurveFit or FuncFit to allow Igor to finalize the change to the X axis range.

If you call CurveFit or FuncFit from a user-defined function and use the /D flag, which turns on the auto-destination feature, then the fit curve will not update until all running functions in the call chain return. If it is important that the graph displaying the destination wave reflect the fit result before functions return, you must call DoUpdate.

### *See Also* {#see-also}
[Curve Fitting](/igorpro/analysis/curve-fitting.md), [Special Variables for Curve Fitting](/igorpro/analysis/curve-fitting.md#special-variables-for-curve-fitting), [Fitting with Constraints](/igorpro/analysis/curve-fitting.md#fitting-with-constraints), [Accessing Variables Used by Igor Operations](/igorpro/programming/macros.md#accessing-variables-used-by-igor-operations)

For fitting to a user-specified function, see [FuncFit](/igorpro/commands/funcfit.md). For fitting to a multivariate user-specified function, see [FuncFit](/igorpro/commands/funcfit.md) and [FuncFitMD](/igorpro/commands/funcfitmd.md). For a detailed description of confidence and prediction bands, see [Confidence Bands and Coefficient Confidence Intervals](/igorpro/analysis/curve-fitting.md#confidence-bands-and-coefficient-confidence-intervals).

### *Demos* {#demos}
[Open Constraint Demo](#igor-pxp/Examples/Curve__Fitting/Constraint__Demo.pxp)

[Open Global Fit Demo](#igor-pxp/Examples/Curve__Fitting/Global__Fit__Demo.pxp)

[Open Multi-Peak Fit Demo](#igor-pxp/Examples/Curve__Fitting/Multi-Peak__Fit.pxp)

[Open Multi-Variate Fit Demo](#igor-pxp/Examples/Curve__Fitting/Multi-Variate__Fit__Demo.pxp)

[Open Multiple Fits In Threads Demo](#igor-pxp/Examples/Curve__Fitting/MultipleFitsInThreads.pxp)