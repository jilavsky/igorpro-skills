---
description: "The Gauss2D function returns the value of a two-dimensional Gaussian peak defined by the coefficients in the wave w."
slug: /commands/gauss2d
---

<div className="command-signature">

## <strong>Gauss2D</strong> (<em>w</em>, <em>x</em>, <em>y</em>) {#gauss2d}

</div>

The Gauss2D function returns the value of a two-dimensional Gaussian peak defined by the coefficients in the wave *w*. The equation is the same as the Gauss2D curve fit:



$$
\displaystyle w[0]+w[1] \exp \left\{\frac{-1}{2\left(1-w[6]^{2}\right)}\left[\left(\frac{x-w[2]}{w[3]}\right)^{2}+\left(\frac{y-w[4]}{w[5]}\right)^{2}-\left(\frac{2 w[6](x-w[2])(y-w[4])}{w[3] w[5]}\right)\right]\right\} .
$$

### *Examples* {#examples}
Do a fit to a Gaussian peak in a portion of a wave, then extend the model trace to the rest of the X range (watch out for the very long wave assignment to junkg2D):


```igor
Make/O/N=(100,100) junkg2D	// fake data wave
Setscale/I x -1,1,junkg2D
Setscale/I y -1,1,junkg2D
Display; AppendImage junkg2D
junkg2D = -1 + 2.5*exp((-1/(2*(1-.4^2)))*(((x-.1)/.2)^2+((y+.2)/.35)^2+2*.4*((x-.1)/.2)*((y+.2)/.35)))
junkg2D += gnoise(.01)
Duplicate/O junkg2D, junkg2Dfit
junkg2Dfit = NaN
AppendMatrixContour junkg2Dfit
CurveFit gauss2D  junkg2D[20,80][10,70] /D=junkg2Dfit[20,80][10,70]

// now extend the model trace
junkg2Dfit = Gauss2D(w_coef, x, y)
```