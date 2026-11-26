---
description: "The IFFT operation calculates the Inverse Discrete Fourier Transform of srcWave using a multidimensional fast prime factor decomposition algorithm."
slug: /commands/ifft
---

<div className="command-signature">

## <strong>IFFT</strong>  [<em>flags</em>] <em>srcWave</em> {#ifft}

</div>

The IFFT operation calculates the Inverse Discrete Fourier Transform of *srcWave* using a multidimensional fast prime factor decomposition algorithm. This operation is the inverse of the [FFT](/igorpro/commands/fft.md) operation.

### *Output Wave Name* {#output-wave-name}
For compatibility with earlier versions of Igor, if you use IFFT without /ROWS or /COLS, the operation overwrites *srcWave*.

If you use the /ROWS flag, IFFT uses the default output wave name M_RowFFT and if you use the /COLS flag, IFFT uses the default output wave name M_ColFFT.

We recommend that you use the /DEST flag to make the output wave explicit and to prevent overwriting *srcWave*.

### *Parameters* {#parameters}
*srcWave* is a complex wave. The IFFT of *srcWave* is a either a real or complex wave, according to the length and flags.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C</span> | Forces the result of the IFFT to be complex. Normally, the IFFT produces a real result unless certain special conditions are detected as described below. |
| <span class="table-cell-nowrap">/COLS</span> | Computes the 1D IFFT of 2D *srcWave* one column at a time, storing the results in the destination wave. You must specify a destination wave using the /DEST flag (no other flags are allowed). See the /ROWS flag and corresponding flags of the [FFT](/igorpro/commands/fft.md) operation. |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the output wave created by the IFFT operation. |
|  | It is an error to specify the same wave as both *srcWave* and *destWave*. |
|  | When used in a function, the IFFT operation by default creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave*, as specified by /DEST, is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/R</span> | Forces real output when, due to a power of 2 number of points, IFFT would otherwise automatically produce a complex result. |
| <span class="table-cell-nowrap">/ROWS</span> | Calculates the IFFT of only the first dimension of 2D *srcWave*. It computes the 1D FFT one row at a time. You must specify a destination wave using the /DEST flag (no other flags are allowed). See the /COLS flag and corresponding flags of the [FFT](/igorpro/commands/fft.md) operation. |
| <span class="table-cell-nowrap">/Z</span> | Will not rotate *srcWave* when computing the IDFT of a complex wave whose length is an integral power of 2. |
|  | This length indicates that the Inverse DFT result will also be a complex wave. When the result is complex, ***and*** the x scaling of *srcWave* is such that the first point is ***not*** x=0, it normally rotates *srcWave* by -N/2 points before performing the IFFT. This inverts the process of performing an FFT on a complex wave. However, when /Z is specified, it does not perform this rotation. |

### *Details* {#details}
The data type of *srcWave* must be complex. You should be aware that an IFFT on a number of points that is prime can be slow.

By default, the IFFT assumes you are performing an inverse transform on data that was originally real and therefore it produces a real result. However, for historical and compatibility reasons, Igor detects the special conditions of a one-dimensional wave containing an integral power of 2 data points. It then automatically creates a complex result.

When the result is complex, the number of points (N) in the resulting wave will be of the same length. Otherwise the resulting wave will be real and of length (N-1)*2.

In either the complex or real case the X units of the output wave  are changed to "s". The X scaling also is changed appropriately, cancelling out the adjustments made by the FFT operation. When the data is multidimensional, the same considerations apply to the additional dimensions. The scaling description and IDFT equation below pretend that the IFFT is not performed in-place. After computing the IFFT values, the X scaling of *waveOut* is changed as if Igor had executed these commands:


```igor
Variable points	// time-domain points, NtimeDomain
if( waveIn was complex wave )
	points= numpnts(waveIn)
else                                            // waveIn was real wave
	points= (numpnts(waveIn) - 1) * 2	
endif
Variable deltaT= 1 / (points*deltaX(waveIn))    // 1/(NtimeDomainΔx)
SetScale/P waveOut 0,deltaT,"s"
```

The IDFT equation is:

$$
\displaystyle { waveOut }[n]=\frac{1}{N} \sum_{k=0}^{N-1} { waveIn }[k] \exp \left(\frac{2 \pi i k n}{N}\right), \quad \text { where } \quad i=\sqrt{-1} .
$$

### *See Also* {#see-also}

[Fourier Transforms](/igorpro/analysis/signal-processing.md#fourier-transforms) in in the Signal Processing help file for an example that compares the FFT result with the continuous Fourier transform values.

[FFT](/igorpro/commands/fft.md), [DSPPeriodogram](/igorpro/commands/dspperiodogram.md), [MatrixOp](/igorpro/commands/matrixop.md)

### *Demos* {#demos}
[Open FFT Swapping Demo](#igor-pxp/Examples/Analysis/FFT__Swapping__Demo.pxp)