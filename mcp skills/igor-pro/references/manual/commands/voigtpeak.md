---
description: "The VoigtPeak function returns a value from a Voigt peak shape defined by coefficients in wave w at location x. It was added in Igor Pro 8.00."
slug: /commands/voigtpeak
---

<div className="command-signature">

## <strong>VoigtPeak</strong> (<em>w</em>, <em>x</em>) {#voigtpeak}

</div>

The VoigtPeak function returns a value from a Voigt peak shape defined by coefficients in wave *w* at location *x*. It was added in Igor Pro 8.00.

The Voigt peak shape is defined as a convolution of a Gaussian and a Lorenztian peak. We use an approximation that is described by the author as having "accuracy typically at least 13 significant digits". This function is equivalent to the built-in Voigt fitting function. See [Built-in Curve Fitting Functions](/igorpro/analysis/curve-fitting.md#built-in-curve-fitting-functions).

The coefficients are:


|  |  |
| --- | --- |
| *w*[0]: | Vertical offset. |
| *w*[1]: | Peak area. |
| *w*[2]: | Peak center location. |
| *w*[3]: | Gaussian component width expressed as Full Width at Half Max (FWHM). |
| *w*[4]: | Ratio of Lorenztian component width to the Gaussian component width. For w[4]=0, the peak shape is purely Gaussian, as w[4] → ∞, the peak shape become purely Lorenztian. A value of 1 results in Gaussian and Lorenztian components of equal width. |

### *References* {#references}
The code used to compute VoigtPeak was written by Steven G. Johnson of MIT. You can learn more about it at [http://ab-initio.mit.edu/Faddeeva](http://ab-initio.mit.edu/Faddeeva).

### *See Also* {#see-also}
[VoigtFunc](/igorpro/commands/voigtfunc.md), [Faddeeva](/igorpro/commands/faddeeva.md), [Built-in Curve Fitting Functions](/igorpro/analysis/curve-fitting.md#built-in-curve-fitting-functions)