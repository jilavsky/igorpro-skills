---
description: "The DSPDetrend operation removes from srcWave a trend defined by the best fit of the specified function to the data in srcWave."
slug: /commands/dspdetrend
---

<div className="command-signature">

## <strong>DSPDetrend</strong>  [/F=<em>function</em> /M=<em>maskWave</em> /P=<em>polyOrder</em> /Q]  <em>srcWave</em> {#dspdetrend}

</div>

The DSPDetrend operation removes from *srcWave*  a trend defined by the best fit of the specified function to the data in srcWave.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Subtracts the average of *srcWave*  before performing any fitting. Added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the main output wave created by the the operation replacing either W_Detrend or M_Detrend depending on dimensionality. |
| <span class="table-cell-nowrap">/F = *function*</span> | *function* is one of the built-in curve fitting functions: |
|  | gauss, lor, exp, dblexp, sin, line, poly (requires /P), hillEquation, sigmoid, power, lognormal, poly2d (requires /P), gauss2d. |
|  | If *function* is unspecified, the defaults are line if *srcWave*  is 1D or poly2d if *srcWave*  is 2D. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave*, as specified by /DEST, is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/M = *maskWave*</span> | Detrending will only affect points that are nonzero in *maskWave*. Note that *maskWave* must have the same dimensionality as *srcWave*. |
| <span class="table-cell-nowrap">/P = *n*</span> | Specifies polynomial order for poly or poly2d functions (see [CurveFit](/igorpro/commands/curvefit.md) for details). |
|  | When used with the 1D poly function *n*  specifies the number of terms in the polynomial. |
|  | By default *n* =3 for the 1D case and *n* =1 for poly2d. |
| <span class="table-cell-nowrap">/Q</span> | No error reporting; quiet mode. |

### *Details* {#details}
DSPDetrend sets V_flag to zero when the operation succeeds, otherwise it will be set to -1 or will contain an error code from the curve fitting routines. Results are saved in the wave W_Detrend (for 1D input) or M_Detrend (2D input) in the current data folder. If a wave by that name already exists in the current data folder it will be overwritten.

### *See Also* {#see-also}
[CurveFit](/igorpro/commands/curvefit.md) for more information about V_FitQuitReason and the built-in fitting functions.