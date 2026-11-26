---
description: "VoigtFunc computes the Voigt function using an approximation that has an accuracy of, as described by the author, \"typically at least 13 significant digits\"."
slug: /commands/voigtfunc
---

<div className="command-signature">

## <strong>VoigtFunc</strong> (<em>X</em>, <em>Y</em>) {#voigtfunc}

</div>

VoigtFunc computes the Voigt function using an approximation that has an accuracy of, as described by the author, "typically at least 13 significant digits".

VoigtFunc returns values from a normalized Voigt peak centered at X=0 for the given value of X. The X input is a normalized distance from the peak center:

$$
\displaystyle X=\sqrt{\ln (2)} \frac{v-v_{0}}{\gamma_{g}}
$$

where 
$$
\displaystyle \gamma_{g}
$$
 is the Gaussian component half-width, and 
$$
\displaystyle v-v_{0}
$$
 is the distance from the peak center.

The parameter Y is the shape parameter. When Y is zero, the peak is pure Gaussian. When Y approaches infinity, the shape becomes pure Lorentzian. When Y is sqrt(ln(2)), the mix is half-and-half.

VoigtFunc was added in Igor Pro 7.00. The approximation used to compute it was changed Igor 8.00 for greater accuracy.

### *Details* {#details}
The VoigtFunc function returns values from a normalized peak that can be used as the basis for user-defined fitting functions. The function is used as the basis for the built-in Voigt fitting function and the [VoigtPeak](/igorpro/commands/voigtpeak.md) function.

### *VoigtFunc Curve Fitting Example* {#voigtfunc-curve-fitting-example}
Here is an example of a user-defined fitting function built on VoigtFunc:


```igor
Constant sqrtln2=0.832554611157698			// sqrt(ln(2))
Constant sqrtln2pi=0.469718639349826		// sqrt(ln(2)/pi)

Function MyVoigtFit(w,xx) : FitFunc
	Wave w
	Variable xx

	//CurveFitDialog/ These comments were created by the Curve Fitting dialog. Altering them will
	//CurveFitDialog/ make the function less convenient to work with in the Curve Fitting dialog.
	//CurveFitDialog/ Equation:
	//CurveFitDialog/ Variable ratio = sqrtln2/gw
	//CurveFitDialog/ Variable xprime = ratio*(xx-x0)
	//CurveFitDialog/ Variable voigtY = ratio*shape
	//CurveFitDialog/ f(xx) = y0 + area*sqrtln2pi*VoigtFunc(xprime, voigtY)
	//CurveFitDialog/ End of Equation
	//CurveFitDialog/ Independent Variables 1
	//CurveFitDialog/ xx
	//CurveFitDialog/ Coefficients 5
	//CurveFitDialog/ w[0] = y0
	//CurveFitDialog/ w[1] = area
	//CurveFitDialog/ w[2] = x0
	//CurveFitDialog/ w[3] = gw (FWHM)
	//CurveFitDialog/ w[4] = shape (Lw/Gw)

	Variable voigtX = 2*sqrtln2*(xx-w[2])/w[3]
	Variable voigtY = sqrtln2*w[4]
	return w[0] + (w[1]/w[3])*2*sqrtln2pi*VoigtFunc(voigtX, voigtY)
End
```

Parameter w[0] sets the vertical offset, w[1] sets the peak area, w[2] sets the location of the peak, w[3] gives the Gaussian component's full width at half max and w[4] is the ratio of the Lorenztian width to the Gaussian width.

After the fit, assuming you used a coefficient wave named voigtCoefs, you can calculate the width of the full Voigt peak as follows:


```igor
Variable/G wl = voigtCoefs[4]*voigtCoefs[3]
Variable/G wg = voigtCoefs[3]
Variable wv = wl/2 + sqrt( wl^2/4 + wg^2)
```

### *References* {#references}
The code used to compute the VoigtFunc was written by Steven G. Johnson of MIT. You can learn more about it at [http://ab-initio.mit.edu/Faddeeva](http://ab-initio.mit.edu/Faddeeva).

### *See Also* {#see-also}
[VoigtPeak](/igorpro/commands/voigtpeak.md), [VoigtFunc](/igorpro/commands/voigtfunc.md), [Built-in Curve Fitting Functions](/igorpro/analysis/curve-fitting.md#built-in-curve-fitting-functions)