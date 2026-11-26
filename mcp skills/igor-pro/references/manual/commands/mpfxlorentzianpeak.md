---
description: "The MPFXLorentzianPeak function implements a single Lorentzian peak with no Y offset in the format of an all-at-once fitting function."
slug: /commands/mpfxlorentzianpeak
---

<div className="command-signature">

## <strong>MPFXLorentzianPeak</strong> (<em>cw</em>, <em>yw</em>, <em>xw</em>) {#mpfxlorentzianpeak}

</div>

The MPFXLorentzianPeak function implements a single Lorentzian peak with no Y offset in the format of an all-at-once fitting function. It fills the wave *yw* with values defined by a Lorentzian peak as if this wave assignment statement was executed:


```igor
yw = 2*cw[2]/pi * cw[1]/(4*(xw-cw[0])^2 + cw[1]^2)
```

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *cw* | Coefficient wave. The Lorentzian peak shape is defined by the coefficients as follows: |
|  |<table class="nested-table"><tbody><tr><td>cw[0]:</td><td>Peak location.</td></tr><tr><td>cw[1]:</td><td>Peak width as full width at half maximum.</td></tr><tr><td>cw[2]:</td><td>Peak area.</td></tr></tbody></table>
|  | *cw* must be a double precision wave. |
| *yw* | Y wave into which values are stored. |
|  | *yw* may be either double precision or single precision. |
| *xw* | X wave containing the X values at which the peak function is to be evaluated. |
|  | *xw* may be either double precision or single precision. |

### *Details* {#details}
This function is primarily intended to support the Multipeak Fitting package. To use MPFXLorentzianPeak as a fitting function, wrap it in an all-at-once user-defined fitting function:


```igor
Function FitLorentzianPeak(Wave cw, Wave yw, Wave xw) : FitFunc
	Variable dummy = MPFXLorentzianPeak(cw, yw, xw)
End
```

The assignment to "dummy" is required because you must explicitly do something with the return value of a built-in function.

If the waves do not satisfy the number type requirements, the function returns NaN. A successful invocation returns zero.

### *See Also* {#see-also}
[All-At-Once Fitting Functions](/igorpro/analysis/curve-fitting.md#all-at-once-fitting-functions)