---
description: "The MPFXEMGPeak function implements a single exponentially modified Gaussian peak with no Y offset in the format of an all-at-once fitting function."
slug: /commands/mpfxemgpeak
---

<div className="command-signature">

## <strong>MPFXEMGPeak</strong> (<em>cw</em>, <em>yw</em>, <em>xw</em>) {#mpfxemgpeak}

</div>

The MPFXEMGPeak function implements a single exponentially modified Gaussian peak with no Y offset in the format of an all-at-once fitting function. The exponentially modified Gaussian peak shape is a convolution of an exponential and a Gaussian peak.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *cw* | Coefficient wave, which must be a double-precision wave. |
|  | The Gaussian peak shape is defined by the coefficients as follows: |
|  |<table class="nested-table"><tbody><tr><td>cw[0]:</td><td>Peak location. This is actually the location of the underlying Gaussian peak. There is no analytic expression for the actual peak location.</td></tr><tr><td>cw[1]:</td><td>Standard deviation of the Gaussian portion.</td></tr><tr><td>cw[2]:</td><td>Amplitude-related parameter.</td></tr><tr><td>cw[3]:</td><td>Decay constant of the exponential portion.</td></tr></tbody></table>
|  | *cw* must be a double precision wave. |
| *yw* | Y wave into which values are stored. |
|  | *yw* may be either double precision or single precision. |
| *xw* | X wave containing the X values at which the peak function is to be evaluated. |
|  | *xw* may be either double precision or single precision. |

### *Details* {#details}
There is no analytic expression for peak parameters of common interest like the amplitude, location and width. The Multipeak Fitting package uses numerical techniques to get approximations.

This function is primarily intended to support the Multipeak Fitting package.

To use MPFXEMGPeak as a fitting function, wrap it in an all-at-once user-defined fitting function:


```igor
Function FitVoigtPeak(Wave cw, Wave yw, Wave xw) : FitFunc
	Variable dummy = MPFXEMGPeak(cw, yw, xw)
End
```

The assignment to "dummy" is required because you must explicitly do something with the return value of a built-in function.

The implementation of this function involves the [erfcx](/igorpro/commands/erfcx.md) function.

If the waves do not satisfy the number type requirements, the function returns NaN. A successful invocation returns zero.

### *See Also* {#see-also}
[All-At-Once Fitting Functions](/igorpro/analysis/curve-fitting.md#all-at-once-fitting-functions)