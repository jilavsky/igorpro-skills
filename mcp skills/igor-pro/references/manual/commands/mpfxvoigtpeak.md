---
description: "The MPFXVoigtPeak function implements a single Voigt peak with no Y offset in the format of an all-at-once fitting function."
slug: /commands/mpfxvoigtpeak
---

<div className="command-signature">

## <strong>MPFXVoigtPeak</strong> (<em>cw</em>, <em>yw</em>, <em>xw</em>) {#mpfxvoigtpeak}

</div>

The MPFXVoigtPeak function implements a single Voigt peak with no Y offset in the format of an all-at-once fitting function. It fills the wave *yw* with values defined by a Voigt peak as if this wave assignment statement was executed:


```igor
yw = cw[2]*VoigtFunc(cw[1]*(xw-cw[0]), cw[3])
```

The [VoigtFunc](/igorpro/commands/voigtfunc.md) function here is a basic Voigt peak shape, a convolution of a Gaussian and Lorentzian peak shapes. The first parameter of VoigtFunc controls the shape. A value of zero results in a peak shape that is 100% Gaussian. As the first parameter approaches infinity the shape transitions to 100% Lorentzian. At a value of sqrt(ln(2)) ≅ 0.832555 the mix is 50/50.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *cw* | Coefficient wave. The Gaussian peak shape is defined by the coefficients as follows: |
|  |<table class="nested-table"><tbody><tr><td>cw[0]:</td><td>Peak location.</td></tr><tr><td>cw[1]:</td><td>Affects the width; the actual width is a complicated function of cw[1], cw[2], and cw[3].</td></tr><tr><td>cw[2]:</td><td>Amplitude factor; the actual amplitude is affected by the other parameters.</td></tr><tr><td>cw[3]:</td><td>Shape factor. Zero results in pure Gaussian, infinity results in pure Lorentzian, one is 50% Gaussian and 50% Lorentzian.</td></tr></tbody></table>
|  | *cw* must be a double precision wave. |
| *yw* | Y wave into which values are stored. |
|  | *yw* may be either double precision or single precision. |
| *xw* | X wave containing the X values at which the peak function is to be evaluated. |
|  | *xw* may be either double precision or single precision. |

### *Details* {#details}
This function is primarily intended to support the Multipeak Fitting package. For other purposes we recommend the [VoigtPeak](/igorpro/commands/voigtpeak.md) function which has more convenient parameters.

To use MPFXVoigtPeak as a fitting function, wrap it in an all-at-once user-defined fitting function:


```igor
Function FitVoigtPeak(Wave cw, Wave yw, Wave xw) : FitFunc
	Variable dummy = MPFXVoigtPeak(cw, yw, xw)
End
```

The assignment to "dummy" is required because you must explicitly do something with the return value of a built-in function.

If the waves do not satisfy the number type requirements, the function returns NaN. A successful invocation returns zero.

### *References* {#references}
The code used to compute VoigtPeak was written by Steven G. Johnson of MIT. You can learn more about it at [http://ab-initio.mit.edu/Faddeeva](http://ab-initio.mit.edu/Faddeeva).

### *See Also* {#see-also}
[All-At-Once Fitting Functions](/igorpro/analysis/curve-fitting.md#all-at-once-fitting-functions), [VoigtPeak](/igorpro/commands/voigtpeak.md), [VoigtFunc](/igorpro/commands/voigtfunc.md)