---
description: "The FuncFitMD operation performs a curve fit to the multivariate user defined function specified by fitFuncName."
slug: /commands/funcfitmd
---

<div className="command-signature">

## <strong>FuncFitMD</strong>  [ <em>flags</em> ] <em>fitFuncName</em>, <em>cwaveName</em>, <em>waveName</em>  [ <em>flag</em> <em>parameters</em> ] {#funcfitmd}

</div>

The FuncFitMD operation performs a curve fit to the multivariate user defined function specified by *fitFuncName*. FuncFitMD handles gridded datasets in multidimensional waves. Most parameters and flags are the same as for the [CurveFit](/igorpro/commands/curvefit.md) and [FuncFit](/igorpro/commands/funcfit.md) operations; differences are noted below.

FuncFitMD operation parameters are grouped in the following categories: flags, parameters (*fitFuncName*, *cwaveName*, *waveName*), and flag parameters. The sections below correspond to these categories. Note that flags must precede the *fitFuncName* and flag parameters must follow *waveName*.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/L = *dimSize*</span> | Sets the dimension size of the wave created by the auto-trace feature, that is, /D without destination wave. The wave fit_*waveName* will be a multidimensional wave of the same dimensionality as *waveName* that has *dimSize* elements in each dimension. That is, if you are fitting to a matrix wave, fit_*waveName* will be a square matrix that has dimensions *dimSize* x *dimSize*.<br><div><Admonition type="caution"><p>*dimSize* =100 requires 100 million points for a 4-dimensional wave!</p></Admonition></div> |

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *fitFuncName* | User-defined function to fit to, which must be a function taking 2 to 4 independent variables. |
| *cwaveName* | 1D wave containing the fitting coefficients. |
| *waveName* | The wave containing the dependent variable data to be fit to the specified function. For functions of just one independent variable, the dependent variable data is often referred to as "Y data". You can fit to a subrange of the wave by supplying (*startX*,*endX*) or [*startP*,*endP*] for each dimension after the wave name. See ***Wave Subrange Details*** below for more information on subranges of waves in curve fitting. |

### *Flag Parameters* {#flag-parameters}

These flag parameters must follow waveName.

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/AD[ = *doAutoDest* ]</span> | If *doAutoDest* is 1, it is the same as /D alone. /AD is the same as /AD=1. See [CurveFit](/igorpro/commands/curvefit.md) for details. |
| <span class="table-cell-nowrap">/AR = *doAutoResid*</span> | If *doAutoResid* is 1, it is the same as /R alone. /AR is the same as /AR=1. See [CurveFit](/igorpro/commands/curvefit.md) for details. |
| <span class="table-cell-nowrap">/E = *epsilonWaveName*</span> | Specifies a wave containing epsilon values used to calculate numerical estimates of derivatives of the fitting function. Each element of the epsilon wave specifies the change in the corresponding coefficient used to numerically estimate the partial derivative with respect to that coefficient. The epsilon wave must have the same number of points as the coefficient wave. See [The Epsilon Wave](/igorpro/analysis/curve-fitting.md#the-epsilon-wave) in the Curve Fitting help topic for details. |
| <span class="table-cell-nowrap">/T = *twaveName*</span> | Like /X except for the T independent variable. This is a 1D wave having as many elements as *waveName* has chunks. |
| <span class="table-cell-nowrap">/X = *xwaveName*</span> | X independent variable values for the data to fit come from *xwaveName* instead of from the X scaling of *waveName*. This is a 1D wave having as many elements as *waveName* has rows. |
| <span class="table-cell-nowrap">/Y = *ywaveName*</span> | Like /X except for the Y independent variable. This is a 1D wave having as many elements as *waveName* has columns. |
| <span class="table-cell-nowrap">/Z = *ywaveName*</span> | Like /X except for the Z independent variable. This is a 1D wave having as many elements as *waveName* has layers. |
| <span class="table-cell-nowrap">/NWOK</span> | Allowed in user-defined functions only. When present, certain waves may be set to null wave references. Passing a null wave reference to FuncFitMD is normally treated as an error. By using /NWOK, you are telling FuncFitMD that a null wave reference is not an error but rather signifies that the corresponding flag should be ignored. This makes it easier to write function code that calls FuncFitMD with optional waves. |
|  | The waves affected are the X wave or waves (/X), the Y spacing wave (/Y), the Z spacking wave (/Z) the T spacing wave (/T), weight wave (/W), epsilon wave (/E) and mask wave (/M). The destination wave (/D=wave) and residual wave (/R=wave) are also affected, but the situation is more complicated because of the dual use of /D and /R to mean "do autodestination" and "do autoresidual". See /AR and /AD. |
|  | If you don't need the choice, it is better not to include this flag, as it disables useful error messages when a mistake or run-time situation causes a wave to be missing unexpectedly. |
|  | <div><Admonition type="note"><p>To work properly this flag must be the last one in the command.</p></Admonition></div> |

### *Details* {#details}
Auto-residual (/R with no wave specified) and auto-trace (/D with no wave specified) for functions having two independent variables are plotted in a separate graph window if *waveName* is plotted as a contour or image in the top graph. An attempt is made to plot the model values and residuals in the same way as the input data.

By default the auto-trace and auto-residual waves are 50x50 or 25x25x25 or 15x15x15x15. Use /L=*dimSize* for other sizes. Make your own wave and use /D=*waveName* or /R=*waveName* if you want a wave that isn't square. In this case, the wave dimensions must be the same as the dependent data wave.

Confidence bands are not available for multivariate fits.

### *Wave Subrange Details* {#wave-subrange-details}
Almost any wave you specify to FuncFitMD can be a subrange of a wave. The syntax for wave subranges is the same as for the Display command; see [Subrange Display Syntax](/igorpro/graphing/graphs.md#subrange-display-syntax) for details. Note that the dependent variable data (*waveName*) must be a multidimensional wave; this requires an extension of the subrange syntax to allow a multidimensional subrange. See [CurveFit](/igorpro/commands/curvefit.md) ***Wave Subrange Details*** section for a discussion of the use of subranges in curve fitting.

The backwards compatibility rules for CurveFit apply to FuncFitMD as well.

A subrange could be used to pick a plane from a 3D wave for fitting using a fit function taking two independent variables:


```igor
Make/N=(100,100,3) DepData
FuncFitMD fitfunc2D, myCoefs, DepData[][][0] ...
```

### *See Also* {#see-also}
[CurveFit](/igorpro/commands/curvefit.md) for parameter details. See [Fitting to a Multivariate Function](/igorpro/analysis/curve-fitting.md#fitting-to-a-multivariate-function) for the proper form for the *functionName* as well as the use of *cwaveName* and *ewaveName*.