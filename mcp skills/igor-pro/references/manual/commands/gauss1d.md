---
description: "The Gauss1D function returns the value of a Gaussian peak defined by the coefficients in the wave w. The equation is the same as the Gauss curve fit."
slug: /commands/gauss1d
---

<div className="command-signature">

## <strong>Gauss1D</strong> (<em>w</em>, <em>x</em>) {#gauss1d}

</div>

The Gauss1D function returns the value of a Gaussian peak defined by the coefficients in the wave *w.* The equation is the same as the Gauss curve fit:

$$
\displaystyle w[0]+w[1] \exp \left[-\left(\frac{x-w[2]}{w[3]}\right)^{2}\right] .
$$

### *Examples* {#examples}
Do a fit to a Gaussian peak in a portion of a wave, then extend the model trace to the rest of the X range:


```igor
Make/O/N=100 junkg	// fake data wave
Setscale/I x -1,1,junkg
Display junkg
junkg = 1+2.5*exp(-((x-.5)/.3)^2)+gnoise(.1)
Duplicate/O junkg, junkgfit
junkgfit = NaN
AppendToGraph junkgfit
CurveFit gauss  junkg[50,99] /D=junkgfit

// now extend the model trace
junkgfit = Gauss1D(w_coef, x)
```