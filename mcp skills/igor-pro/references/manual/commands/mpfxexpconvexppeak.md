---
description: "The MPFXExpConvExpPeak function implements a single peak with no Y offset in the format of an all-at-once fitting function."
slug: /commands/mpfxexpconvexppeak
---

<div className="command-signature">

## <strong>MPFXExpConvExpPeak</strong> (<em>cw</em>, <em>yw</em>, <em>xw</em>) {#mpfxexpconvexppeak}

</div>

The MPFXExpConvExpPeak function implements a single peak with no Y offset in the format of an all-at-once fitting function. The peak shape is that of an exponential convolved with another exponential.

MPFXExpConvExpPeak is similar to the MPFXEMGPeak, but it has a sharp onset. It fills the wave *yw* with peak values as if a simple wave assignment was executed.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *cw* | Coefficient wave. The Gaussian peak shape is defined by the coefficients as follows: |
|  |<table class="nested-table"><tbody><tr><td>cw[0]:</td><td>Peak location.</td></tr><tr><td>cw[1]:</td><td>Peak height.</td></tr><tr><td>cw[2]:</td><td>Inverse of the decay constant of one exponential.</td></tr><tr><td>cw[3]:</td><td>Inverse of the decay constant of the other exponential.</td></tr></tbody></table>
|  | *cw* must be a double precision wave. |
| *yw* | Y wave into which values are stored. |
|  | *yw* may be either double precision or single precision. |
| *xw* | X wave containing the X values at which the peak function is to be evaluated. |
|  | *xw* may be either double precision or single precision. |

### *Details* {#details}
The following equations and discussion use these definitions:


```igor
c0 = cw[0], c1 = cw[1], c2 = cw[2], c3 = cw[3]
```

The peak location given by c0 is not the actual peak location; it is simply a parameter that offsets the peak in the X direction. The actual location is given by

$$
\displaystyle l o c=\frac{\ln \left(\frac{c 2}{c 3}\right)}{c 2-c 3}+c 0
$$

The actual peak height is given by

$$
\displaystyle h=\frac{c 1 \cdot c 2\left\{\left(\frac{c 2}{c 3}\right)^{-\frac{c 2}{c 2-c 3}}-\left(\frac{c 2}{c 3}\right)^{-\frac{c 3}{c 2-c 3}}\right\}}{c 3-c 2}
$$

The peak area is given by c1/c3.

We are not aware of an analytic expression for the full width at half maximum (FWHM).

This function is primarily intended to support the Multipeak Fitting package.

To use MPFXExpConvExpPeak as a fitting function, wrap it in an all-at-once user-defined fitting function:


```igor
Function FitVoigtPeak(Wave cw, Wave yw, Wave xw) : FitFunc
	Variable dummy = MPFXExpConvExpPeak(cw, yw, xw)
End
```

The assignment to "dummy" is required because you must explicitly do something with the return value of a built-in function.

If the waves do not satisfy the number type requirements, the function returns NaN. A successful invocation returns zero.

### *See Also* {#see-also}
[All-At-Once Fitting Functions](/igorpro/analysis/curve-fitting.md#all-at-once-fitting-functions)