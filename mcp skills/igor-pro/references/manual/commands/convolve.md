---
description: "The Convolve operation convolves srcWaveName with each destination wave, putting the result of each convolution in the corresponding destination wave."
slug: /commands/convolve
---

<div className="command-signature">

## <strong>Convolve</strong>  [/A/C] <em>srcWaveName</em>, <em>destWaveName</em> [, <em>destWaveName</em> ]... {#convolve}

</div>

The Convolve operation convolves *srcWaveName*  with each destination wave, putting the result of each convolution in the corresponding destination wave.

Convolve is not multidimensional aware.  Some multidimensional convolutions are covered by the  [MatrixConvolve](/igorpro/commands/matrixconvolve.md), [MatrixFilter](/igorpro/commands/matrixfilter.md), and [MatrixOp](/igorpro/commands/matrixop.md) operations

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Acausal linear convolution. |
| <span class="table-cell-nowrap">/C</span> | Circular convolution. |

### *Details* {#details}
Convolve performs linear convolution unless the /C or /A flag is used. See [Convolution](/igorpro/analysis/signal-processing.md#convolution) for more details.

Depending on the type of convolution, the destination waves' lengths may increase. *srcWaveName*  is not altered unless it also appears as a destination wave.

If *srcWaveName*  is real-valued, each destination wave must be real-valued and if *srcWaveName*  is complex, each destination wave must be complex, too. Double and single precision waves may be freely intermixed; the calculations are performed in double precision.

The linear convolution equation is:

$$
\displaystyle {destWaveOut}[p]=\sum_{m=0}^{N-1} {destWaveIn}[m] \cdot {srcWave}[p-m]
$$

where *N*  is the number of points in the longer of *destWaveIn* and *srcWave*. For circular convolution, the index [*p* -*m* ] is wrapped around when it exceeds the range of [0,numpnts(*srcWave* )-1]. For acausal convolution, when [*p* -*m* ] exceeds the range a zero value is substituted for *srcWave* [*p* -*m* ]. Similar operations are applied to *destWaveIn* [*m* ].

Another way of looking at this equation is that, for all *p*, *destWaveOut*[*p*] equals the sum of the point-by-point products from 0 to p of the destination wave and an end-to-end reversed copy of the source wave that has been shifted to the right by *p*.

The following diagram shows the reversed/shifted srcWave that would be combined with *destWaveIn*. The points numbered 0 through 4 of the reversed *srcWave* would be multiplied with *destWaveIn*[0...4] and summed to produce *destWaveOut*[4]:

<img src="Images/Convolve/Convolve_3.png" width="100%"/>

For linear and acausal convolution, the destination wave is first zero-padded by one less than the length of the source wave. This prevents the "wrap-around" effect that occurs in circular convolution. The zero-padded points are removed after acausal convolution, and retained after linear convolution. The X scaling of the waves is ignored.

The convolutions are performed by transforming the source and destination waves with the Fast Fourier Transform, multiplying them in the frequency domain, and then inverse-transforming them into the destination wave(s).

The convolution is performed in segments if the resulting wave has more than 256 points and the destination wave has twice as many points as the source wave. For acausal convolution, the length of the resulting wave is considered to be numpnts(*srcWaveName*)+numpnts(*destWaveName*)-1 for this calculation.

### *Applications* {#applications}
The usual application of convolution is to compute the response of a linear system defined by its impulse response to an input signal. *srcWaveName* would contain the impulse response, and the destination wave would initially contain the input signal. After the Convolve operation has completed, the destination wave contains the output signal.

Use linear convolution when the source wave contains an impulse response (or filter coefficients) where the first point of *srcWaveName*  corresponds to no delay (*t* = 0).

Use circular convolution for the case where the data in *srcWaveName*  and *destWaveName*  are considered to endlessly repeat (or "wrap around" from the end back to the start), which means no zero padding is needed.

Use acausal convolution when the source wave contains an impulse response where the middle point of *srcWaveName*  corresponds to no delay (*t* = 0).

### *See Also* {#see-also}
[Correlate](/igorpro/commands/correlate.md), [Convolution](/igorpro/analysis/signal-processing.md#convolution),  [MatrixOp](/igorpro/commands/matrixop.md)

### *References* {#references}
A very complete explanation of circular and linear convolution can be found in sections 2.23 and 2.24 of Rabiner and Gold, *Theory and Application of Digital Signal Processing*, Prentice Hall, 1975.