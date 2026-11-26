---
description: "The WindowFunction operation multiplies a 1D (real or complex) srcWave by the named window function."
slug: /commands/windowfunction
---

<div className="command-signature">

## <strong>WindowFunction</strong>  [/FFT[=<em>f</em>  ] /DEST=<em>destWave</em> ] <em>windowKind</em>, <em>srcWave</em> {#windowfunction}

</div>

The WindowFunction operation multiplies a 1D (real or complex) *srcWave* by the named window function.

By default the result overwrites *srcWave*.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *srcWave* | A one-dimensional wave of any numerical type. See [ImageWindow](/igorpro/commands/imagewindow.md) for windowing two-dimensional data. |
| *windowKind* | Specifies the windowing function. Choices for *windowKind* are: |
|  | Bartlett, Blackman367, Blackman361, Blackman492, Blackman474, Cos1, Cos2, Cos3, Cos4, Hamming, Hanning, KaiserBessel20, KaiserBessel25, KaiserBessel30, Parzen, Poisson2, Poisson3, Poisson4, Riemann, and an assortment of flat-top windows listed under [FFT](/igorpro/commands/fft.md). |
|  | See [FFT](/igorpro/commands/fft.md) for window equations and details. The equations assume that /FFT=1. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Creates or overwrites *destWave* with the result of the multiplication of *srcWave* and the window function. |
|  | When used in a function, the WindowFunction operation by default creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/FFT [ = 1]</span> | The window interval is 0...N=numpnts(srcWave). This sets the first value of *srcWave* to zero, but not the last value. This is appropriate for windowing data in preparation for [Fourier Transforms](/igorpro/analysis/signal-processing.md#fourier-transforms), and is the same algorithm used by [FFT](/igorpro/commands/fft.md). |
|  | If /FFT is missing or /FFT=0, the window interval is 0...N=numpnts(srcWave)-1. This sets the first and last value of *srcWave* to 0. This is the (only) algorithm that the [Hanning](/igorpro/commands/hanning.md) operation uses. |

### *Details* {#details}
A "window function" alters the input data by decreasing values near the start and end of the data smoothly towards zero, so that when the [FFT](/igorpro/commands/fft.md) of the data is computed the effects of nonintegral-periodic signals are diminished. This improves the ability of the FFT to distinguish among closely-spaced frequencies. Each window function has advantages and disadvantages, usually trading off rejection of "leakage" against the ability to discriminate adjacent frequencies. For more details, see the References.

WindowFunction stores the window function's normalization value (the average squared window value) in V_value. This is the value you would get from [WaveStats](/igorpro/commands/wavestats.md)'s V_rms*V_rms for a wave of *sricWave*'s length whose values were all equal to 1:


```igor
Make/O data = 1
WindowFunction Bartlet, data    // Bartlet allowed as synonym for Bartlett
Print V_value                   // Prints 0.330709, mean of squared window values
```

<img src="Images/WindowFunction/WindowFunction_0.png" width="100%">


```igor
WaveStats/Q data
Print V_rms*V_rms               // Prints 0.330709
```

### *See Also* {#see-also}
[ImageWindow](/igorpro/commands/imagewindow.md), [FFT](/igorpro/commands/fft.md), [DPSS](/igorpro/commands/dpss.md)

### *References* {#references}
For more information about the use of window functions see:

Harris, F.J., "On the use of windows for harmonic analysis with the discrete Fourier Transform", *Proc, IEEE*, *66*, 51-83, 1978.

Online Wikipedia entry: [http://en.wikipedia.org/wiki/Window_function](http://en.wikipedia.org/wiki/Window_function).