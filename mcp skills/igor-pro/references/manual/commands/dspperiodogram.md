---
description: "The DSPPeriodogram operation calculates the periodogram, cross-spectral density or the degree of coherence of the input waves."
slug: /commands/dspperiodogram
---

<div className="command-signature">

## <strong>DSPPeriodogram</strong>  [/DB /DBR=<em>ref</em>  /COHR /DLSG /NODC=<em>val</em>  /NOR=<em>value</em>  /Q /SEGN={<em>ptsPerSegment</em> , <em>overlapPts</em> } /R=[<em>start</em>, <em>end</em> ] /R=(<em>startX</em>, <em>endX</em>) /WIN=<em>windowKind</em>  /Z ] <em>srcWave</em> [, <em>srcWave2</em> ] {#dspperiodogram}

</div>

The DSPPeriodogram operation calculates the periodogram, cross-spectral density or the degree of coherence of the input waves. The result of the operation is stored in the wave W_Periodogram in the current data folder or in the wave that you specify using the /DEST flag.

To compute the cross-spectral density or the degree of coherence, you need to specify the second wave using the optional *srcWave2* parameter. In this case, W_Periodogram will be complex and the /DB and /DBR flags do not apply.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DB</span> | Expresses results in dB using the maximum value as reference. |
| <span class="table-cell-nowrap">/DBR = *ref*</span> | Expresses the results in dB using the specified *ref* value. |
| <span class="table-cell-nowrap">/COHR</span> | Computes the degree of coherence. This flag applies when the input consists of two waves. |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> | Specifies the output wave created by the operation. |
|  | The /DEST flag was added in Igor Pro 8.00. |
|  | It is an error to specify the same wave as both *srcWave* and *destWave*. |
|  | When used in a function, the DSPPeriodogram operation by default creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/DLSG</span> | When computing the periodogram, cross-spectral density or the degree of coherence using multiple segments the operation by default pads the last segment with zeros as necessary. If you specify this flag, an incomplete last segment is dropped and not included in the calculation. |
| <span class="table-cell-nowrap">/DTRD</span> | Detrends segments by subtracting the linear regression of each segment before multiplication by the window function. /DTRD affects segments and is not compatible with /NODC=1. /DTRD was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave*, as specified by /DEST, is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/NODC = *val*</span> | Suppresses the DC term |
|  |<table class="nested-table"><tbody><tr><td>*val*=1:</td><td>Removes the DC by subtracting the average value of the signal before processing and before applying any window function (see /Win below).</td></tr><tr><td>*val*=2:</td><td>Suppresses the DC term by setting it equal to the second term in the FFT array.</td></tr><tr><td>*val*=0:</td><td>Computes the DC term by the FFT (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/NOR = *N*</span> | Sets the normalization, N, in the periodogram equation. By default, it is the number of data points times the square norm of the window function (if any). |
|  | *N* = 0 or 1: Skips default normalization. |
|  | Any other value of *N* is used as the only normalization. |
| <span class="table-cell-nowrap">/PARS</span> | Sets the normalization to satisfy Parseval's theorem even when using a window function. |
|  | The /PARS flag was added in Igor Pro 8.00. It overrides the /NOR flag. |
|  | See ***Normalization Satisfying Parseval's Theorem*** below for further information. |
| <span class="table-cell-nowrap">/Q</span> | Quiet mode; suppresses printing in the history area. |
| <span class="table-cell-nowrap">/R = [*startPt*, *endPt* ]</span> | Calculates the periodogram for a specified wave range. *startPt* and *endPt* are expressed in terms of point numbers of the source wave. |
| <span class="table-cell-nowrap">/R = (*startX*, *endX* )</span> | Calculates the periodogram for a specified wave range. *startX* and *endX* are expressed in terms of x-values. Note that this option will convert your x-specifications to point numbers and some roundoff may occur. |
| <span class="table-cell-nowrap">/SEGN = {*ptsPerSegment* *, overlapPts* }</span> |  |
|  | Use this flag to compute the periodogram, cross-spectral density or degree of coherence by averaging over multiple segments taken from the input waves. The size of each interval is *ptsPerSegment* . *overlapPts* determines the number of points at the end of each interval that are included in the next segment. |
| <span class="table-cell-nowrap">/WIN = *windowKind*</span> | If you omit the /W flag, the operation uses a rectangular window for the full wave or the range of data selected by the /R flag. |
|  | In the following definitions, *w*(*n*) is the value of the window function that multiplies the signal, *N* is the number of points in the signal wave (or range if /R is specified), and *n* is the wave point index. When using /R, *n* =0 for the first datum in the range. |
|  | Choices for *windowKind* are: |
|  | Bartlett, Blackman367, Blackman361, Blackman492, Blackman474, Cos1, Cos2, Cos3, Cos4, Hamming, Hanning, KaiserBessel20, KaiserBessel25, KaiserBessel30, Parzen, Poisson2, Poisson3, Poisson4, and Riemann. |
|  | See [FFT](/igorpro/commands/fft.md) for window equations and details. |
| <span class="table-cell-nowrap">/Z</span> | Do not report errors. When an error occurs, V_flag is set to -1. |

### *Details* {#details}
The default periodogram is defined as

$$
\displaystyle \text { Periodogram }=\frac{|F(s)|^{2}}{N},
$$

where *F* (s) is the Fourier transform of the signal s and N is the number of points.

In most practical situations you need to account for using a window function (when computing the Fourier transform) which takes the form

$$
\displaystyle \text { Periodogram }=\frac{|F(s \cdot w)|^{2}}{N_{p} N_{w}},
$$

where w is the window function, N<sub>p</sub> is the number of points and N<sub>w</sub> is the normalization of the window function.

If you compute the periodogram by subdividing the signal into multiple segments (with any overlap) and averaging the results over all segments, the expression for the periodogram is

$$
\text { Periodogram }=\frac{\displaystyle \sum_{i=1}^{M}\left|F\left(s_{i} \cdot w\right)\right|^{2}}{M N_{s} N_{w}} \text {, }
$$

where s<sub>i</sub> is the ith segment s, N<sub>s</sub> is the number of points per segment and M is the number of segments.

When calculating the cross-spectral density (csd) of two waves s<sub>1</sub> and s<sub>2</sub>, the operation results in a complex valued wave

$$
\displaystyle c s d=\frac{F\left(s_{A}\right)\left[F\left(s_{B}\right)\right]^{*}}{N},
$$

which contains the normalized product of the Fourier transform of the first wave S<sub>A</sub> with the complex conjugate of the Fourier transform of the second wave S<sub>B</sub>. The extension of the csd calculation to segment averaging has the form

$$
c s d=\frac{\displaystyle \sum_{i=0}^{M} F\left(s_{A i}\right)\left[F\left(s_{B i}\right)\right]^{*}}{M N_{s} N_{w}},
$$

where S<sub>Ai </sub>is the ith segment of the first wave, M is the number of segments and N<sub>s</sub> is the number of points in a segment.

The degree of coherence is a normalized version of the cross-spectral density. It is given by

$$
\gamma=\frac{\displaystyle \sum_{i=0}^{M} F\left(s_{A i}\right)\left[F\left(s_{B i}\right)\right]^{*}}{\displaystyle \sqrt{\sum_{i=0}^{M} F\left(s_{A i}\right)\left[F\left(s_{A i}\right)\right]^{*} \sum_{i=0}^{M} F\left(s_{B i}\right)\left[F\left(s_{B i}\right)\right]^{*}}} .
$$

The bias in the degree of coherence is calculated using the approximation

$$
\displaystyle B=\frac{1}{M}\left[1-|\gamma|^{2}\right]^{2} .
$$

The bias is stored in the wave W_Bias.

If you use the /SEGN flag the actual number of segments is reported in the variable V_numSegments.

Note that DSPPeriodogram does not test the dimensionality of the wave; it treats the wave as 1D. When you compute the cross-spectral density or the degree of coherence the number-type, dimensionality and the scaling of the two waves must agree.

### *Normalization Satisfying Parseval's Theorem* {#normalization-satisfying-parseval-s-theorem}
After executing DSPPeriodogram with the /PARS flag, you can check that the normalization satisfies Parseval's theorem using this function:


```igor
Function CheckNormalization(srcWave, periodogramWave)
	Wave srcWave                        // A real valued time series
	Wave periodogramWave                // e.g., W_Periodogram

	Duplicate/FREE periodogramWave,wp   // Preserve original
	wp[0]/=2                            // Correct the 0 bin
	wp[numpnts(wp)-1] /=2               // Correct the Nyquist bin
	MatrixOP/FREE w2=magsqr(srcWave)/numPoints(srcWave)
	Print sum(wp), sum(w2)              // Parseval: These should be equal
End
```

### *See Also* {#see-also}
The [ImageWindow](/igorpro/commands/imagewindow.md) operation for 2D windowing applications. [FFT](/igorpro/commands/fft.md) for window equations and details.

[Hanning](/igorpro/commands/hanning.md), [LombPeriodogram](/igorpro/commands/lombperiodogram.md), [MatrixOp](/igorpro/commands/matrixop.md)

### *References* {#references}
For more information about the use of window functions see:

Harris, F.J., "On the use of windows for harmonic analysis with the discrete Fourier Transform", *Proc, IEEE*, *66*, 51-83, 1978.

G.C. Carter, C.H. Knapp and A.H. Nuttall, The Estimation of the Magnitude-squared Coherence Function Via Overlapped Fast Fourier Transform Processing, IEEE Trans. Audio and Electroacoustics, V. AU-21, (4) 1973.