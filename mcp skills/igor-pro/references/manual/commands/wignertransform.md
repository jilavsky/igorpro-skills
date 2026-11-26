---
description: "The WignerTransform operation computes the Wigner transformation of a 1D signal in srcWave, which is the name of a real or complex wave."
slug: /commands/wignertransform
---

<div className="command-signature">

## <strong>WignerTransform</strong>  [/Z][/WIDE=<em>wSize</em> ] [/GAUS=<em>gaussianWidth</em> ][/DEST=<em>destWave</em> ] <em>srcWave</em> {#wignertransform}

</div>

The WignerTransform operation computes the Wigner transformation of a 1D signal in *srcWave*, which is the name of a real or complex wave. The result of the WignerTransform is stored in *destWave* or in the wave M_Wigner in the current data folder.

**Flags**


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Creates by default a real wave reference for the destination wave in a user function. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/GAUS = *gWidth*</span> | Computes the Gaussian Wigner Transform, which is a convolution of the Wigner Transform with a two-dimensional Gaussian (in the two parameters of the transform). The computation of the transform simplifies significantly when the product of the widths of the two Gaussians is unity (minimum uncertainty ellipse). |
|  | *gWidth* uses the same units as the *srcWave* scaling. |
| <span class="table-cell-nowrap">/OUT = *type*</span> | Sets the output data type of the standard (not Gaussian) Wigner transform. The following data types are supported: |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Complex</td></tr><tr><td>2:</td><td>Real (default)</td></tr><tr><td>3:</td><td>Magnitude</td></tr><tr><td>4:</td><td>Squared magnitude</td></tr></tbody></table>
|  | /OUT is not allowed with the Gaussian Wigner transform (/GAUS) in which the output is always real. |
|  | The /OUT flag was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">/WIDE = *wSize*</span> | Computes the Wigner Transform and sets the width of the transform to *wSize*. This is the default transformation with *wSize* set to the size of *srcWave*. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The Wigner transform maps a time signal U(t) into a 2D time-frequency representation:

$$
\displaystyle W(t, v)=\int_{-\infty}^{\infty} U\left(t+\frac{x}{2}\right) U^{*}\left(t-\frac{x}{2}\right) e^{-2 \pi i x v} d x .
$$

The computation of the Wigner transform evaluates the offset product:

$$
\displaystyle U\left(t+\frac{x}{2}\right) U^{*}\left(t-\frac{x}{2}\right)
$$

over a finite window and then Fourier transforming the result. The offset product can be evaluated over a finite window width, which can vary from a few elements of the input wave to the full length of the wave. You can control the width of this window using the /WIDE flag. If you do not specify the output destination, WignerTransform saves the results in the wave M_Wigner in the current data folder.

Although the Wigner transform is real, the output will be complex when srcWave is complex. By inspecting the complex wave you can gain some insight into the numerical stability of the algorithm. The X-scaling of the output wave is identical to the scaling of srcWave. The Y-scaling of the input wave is taken from the Fourier Transform of the offset product, which in turn is determined by the X-scaling of srcWave. Specifically, if

```igor
dx=DimDelta(srcWave,0)
```

and *srcWave* has *N* points then 

```igor
dy=DimDelta(M_Wigner,1)=1/(dx*N)
```

WignerTransform does not set the units of the output wave.

The Ambiguity Function is related to the Wigner Transform by a Fourier Transform, and is defined by

$$
\displaystyle A(\tau, v)=\int_{-\infty}^{\infty} U\left(t+\frac{\tau}{2}\right) U^{*}\left(t-\frac{\tau}{2}\right) e^{-2 \pi i t v} d t.
$$

Convolving the Wigner Transform with a 2D Gaussian leads to what is sometimes called the Gaussian Wigner Transform or GWT. Formally the GWT is given by the equation:

$$
\displaystyle G W T\left(t, v ; \delta_{t}, \delta_{v}\right)=\frac{1}{\delta_{t} \delta_{v}} \iint d t^{\prime} d v^{\prime} W\left(t^{\prime}, v^{\prime}\right) \exp \left\{-2 \pi\left[\left(\frac{t-t^{\prime}}{\delta_{t}}\right)^{2}+\left(\frac{v-v^{\prime}}{\delta_{v}}\right)^{2}\right]\right\} .
$$

Computationally this equation simplifies if the respective widths of the two Gaussians satisfy the minimum uncertainty condition δ<sub>t</sub>*δ<sub>ν</sub>=1. The /GAUS flag calculates the Gaussian Wigner Transform using your specified width, δ<sub>t</sub>, and it selects a δ<sub>ν</sub> such that it satisfies the minimum uncertainty condition.

### *References* {#references}
Wigner, E. P., On the quantum correction for thermo-dynamic equilibrium, *Physics Review*, *40*, 749-759, 1932.

Bartelt, H.O., K.-H. Brenner, and A.W. Lohman, The wigner distribution function and its optical production, *Optics Communications*, *32*, 32-38, 1980.

### *See Also* {#see-also}
[CWT](/igorpro/commands/cwt.md), [FFT](/igorpro/commands/fft.md), [WaveTransform](/igorpro/commands/wavetransform.md)

### *Demos* {#demos}
[Open Wigner Demo](#igor-pxp/Examples/Analysis/Wigner__Demo.pxp)