---
description: "The FFT operation computes the Discrete Fourier Transform of srcWave using a multidimensional prime factor decomposition algorithm."
slug: /commands/fft
---

<div className="command-signature">

## <strong>FFT</strong>  [<em>flags</em>]  <em>srcWave</em> {#fft}

</div>

The FFT operation computes the Discrete Fourier Transform of *srcWave* using a multidimensional prime factor decomposition algorithm. By default, *srcWave* is overwritten by the transform.

### *Output Wave Name* {#output-wave-name}
For compatibility with earlier versions of Igor, if you use FFT with no flags or with just the /Z flag, the operation overwrites *srcWave*.

If you use any flag other than /Z, FFT uses default output wave names: W_FFT for a 1D FFT and M_FFT for a multidimensional FFT.

We recommend that you use the /DEST flag to make the output wave explicit and to prevent overwriting *srcWave*.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/COLS</span> | Computes the 1D FFT of 2D *srcWave* one column at a time, storing the results in the destination wave |
|  | $$ \displaystyle I\left[t_{1}\right][n]=\sum_{k=0}^{N-1} f\left[t_{1}\right][k] \exp (i 2 \pi k n / N) . $$ |
|  | You must specify a destination wave using the /DEST flag. No other flags are allowed with this flag. The number of rows must be even. If *srcWave* is a real (NxM) wave, the output matrix will be (1+N/2,M) in analogy with 1D FFT. To avoid changes in the number of points you can convert *srcWave*  to complex data type. This flag applies only to 2D source waves. See also the /ROWS flag. |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the output wave created by the FFT operation. |
|  | It is an error to specify the same wave as both *srcWave* and *destWave*. |
|  | When used in a function, the FFT operation by default creates a complex wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave*, as specified by /DEST, is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/HCC</span> | Hypercomplex transform (cosine). Computes the integral |
|  | $$ \displaystyle I_{c}\left(\omega_{1}, \omega_{2}\right)=\iint_{-\infty}^{\infty} f\left(t_{1}, t_{2}\right) \cos \left(t_{1} \omega_{1}\right) \exp \left(i t_{2} \omega_{2}\right) d t_{1} d t_{2} $$ |
|  | using the 2D FFT (see Details). |
| <span class="table-cell-nowrap">/HCS</span> | Hypercomplex transform (sine). Computes the integral |
|  | $$ \displaystyle I_{s}\left(\omega_{1}, \omega_{2}\right)=\iint_{-\infty}^{\infty} f\left(t_{1}, t_{2}\right) \sin \left(t_{1} \omega_{1}\right) \exp \left(i t_{2} \omega_{2}\right) d t_{1} d t_{2} $$ |
|  | using the 2D FFT (see Details). |
| <span class="table-cell-nowrap">/MAG</span> | Saves just the magnitude of the FFT in the output wave. See comments under /OUT. |
| <span class="table-cell-nowrap">/MAGS</span> | Saves the squared magnitude of the FFT in the output wave.  See comments under /OUT. |
| /OUT=*mode* |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=1:</td><td>Default for complex output.</td></tr><tr><td>*mode*&nbsp;=2:</td><td>Real output.</td></tr><tr><td>*mode*&nbsp;=3:</td><td>Magnitude.</td></tr><tr><td>*mode*&nbsp;=4:</td><td>Magnitude square.</td></tr><tr><td>*mode*&nbsp;=5:</td><td>Phase.</td></tr><tr><td>*mode*&nbsp;=6:</td><td>Scaled magnitude.</td></tr><tr><td>*mode*&nbsp;=7:</td><td>Scaled magnitude squared.</td></tr></tbody></table>
|  | You can also identify modes 2-4 using the convenience flags /REAL, /MAG, and  /MAGS. The convenience flags are mutually exclusive and are overridden by the /OUT flag. |
|  | The scaled quantities apply to transforms of real valued inputs where the output is normally folded in the first dimension (because of symmetry). The scaling applies a factor of 2 to the squared magnitude of all components except the DC. The scaled transforms should be used whenever Parseval's relation is expected to hold. |
| <span class="table-cell-nowrap">/PAD = {*dim1* [, *dim2*, *dim3*, *dim4* ]}</span> |  |
|  | Converts *srcWave* into a padded wave of dimensions *dim1*, *dim2...*. The padded wave contains the original data at the start of the dimension and adds zero entries to each dimension up to the specified dimension size. The *dim1*... values must be greater than or equal to the corresponding dimension size of *srcWave*. If you need to pad just the lowest dimension(s) you can omit the remaining dimensions; for example, /PAD=*dim1* will set *dim2* and above to match the dimensions in *srcWave*. |
| <span class="table-cell-nowrap">/REAL</span> | Saves just the real part of the transform in the output wave. See comments under /OUT. |
| <span class="table-cell-nowrap">/ROWS</span> | Calculates the FFT of only the first dimension of a 2D *srcWave*. It thus computes the 1D FFT of one row at a time, storing the results in the destination wave. |
|  | $$ N[n]\left[t_{2}\right]=\displaystyle \sum_{k=0}^{M-1} f[k]\left[t_{2}\right] \exp (i 2 \pi k n / M) $$ |
|  | You must specify a destination wave using the /DEST flag. No other flags are allowed with this flag. The number of columns must be even. If *srcWave* is a real (NxM) wave, the output matrix will be (N,1+M/2) in analogy with 1D FFT. To avoid changes in the number of points you can convert *srcWave*  to complex data type. See also /COLS flag. |
| <span class="table-cell-nowrap">/RP = [*startPoint*,*endPoint* ]</span> |  |
| <span class="table-cell-nowrap">/RX = (*startX*,*endX* )</span> |  |
|  | Defines a segment of a 1D *srcWave* that will be transformed. By default the operation transforms the whole wave. It is sometimes useful to take advantage of this feature in order to transform just the defined interval, which includes both end points. You can define the interval using wave point indexing with the /RP flag or using the X-values with the /RX flag. The interval must include at least four data points and the total number of points must be an even number. |
| <span class="table-cell-nowrap">/WINF = *windowKind*</span> |  |
|  | Premultiplies a 1D *srcWave* with the selected window function. |
|  | If you include the /PAD flag, the window function is applied to the pre-padded data. |
|  | See Window Functions below for details. |
| <span class="table-cell-nowrap">/Z</span> | Disables rotation of the FFT of a complex wave. Igor normally rotates the FFT result (which is also complex) by N/2 so that x=0 is at the center point (N/2). When /Z is specified, Igor does not perform this rotation and leaves x=0 at the first point (0). |

### *Details* {#details}
The data type of *srcWave* is arbitrary. The first dimension of *srcWave* must be an even number and the minimum length of *srcWave* is four points. When *srcWave*  is a double precision wave, the FFT is computed in double precision. All other data types are transformed using single precision calculations. The result of the FFT operation is always a floating point number (single or double precision).

Depending on your choice of outputs, you may not be able to invert the transform in order to obtain the original *srcWave*.

*srcWave* or any of its intervals must have at least four data points and must not contain NaNs or INFs.

The FFT algorithm is based on prime number decomposition, which decomposes the number of points in each dimension of the wave into a product of prime numbers. The FFT is optimized for primes < 5. In time consuming applications it is frequently worthwhile to pad the data so that the total number of points factors into small prime numbers.

The hypercomplex transforms are computed by writing the sine and cosine as a sum of two exponentials. Let the 2D Fourier transform of the input signal be

$$
\displaystyle F\left[n_{1}\right]\left[n_{2}\right]=\sum_{k_{1}=0}^{N_{1}-1} \sum_{k_{2}=0}^{N_{2}-1} f\left[k_{1}\right]\left[k_{2}\right] \exp \left(i 2 \pi k_{1} \frac{n_{1}}{N_{1}}\right) \exp \left(i 2 \pi k_{2} \frac{n_{2}}{N_{2}}\right)
$$

then the two hypercomplex transforms are given by

$$
\displaystyle I_{c}\left[n_{1}\right]\left[n_{2}\right]=\frac{1}{2}\left(F\left[n_{1}\right][n 2]+F\left[-n_{1}\right][n 2]\right)
$$

and

$$
\displaystyle I_{s}\left[n_{1}\right]\left[n_{2}\right]=\frac{1}{2 i}\left(F\left[n_{1}\right][n 2]-F\left[-n_{1}\right][n 2]\right)
$$

### *Window Functions* {#window-functions}
The /F=*windowKind*  flag premultiplies a 1D *scrWave* with the selected window function.

In the following window definitions, *wn(n)* is the value of the window function that multiplies the signal, *N* is the number of points in the signal wave (or range if /R is specified), and *n* is the wave point index. With /R, *n*=0 for the first datum in the range.

Choices for *windowKind*  are in bold.

**Bartlet**

A synonym for Bartlett.

**Bartlett**

$$
w(n)=\left\{\begin{array}{cc}
\displaystyle \frac{2 n}{N} & n=0,1, \ldots \frac{N}{2} \\
\\
\displaystyle 2-\frac{2 n}{N} & n=\frac{N}{2}, \ldots N-1
\end{array}\right.
$$

**Blackman367, Blackman361,  Blackman492, Blackman474**

$$
\begin{array}{l}
\displaystyle w(n)=a_{0}-a_{1} \cos \left(\frac{2 \pi}{N} n\right)+a_{2} \cos \left(\frac{2 \pi}{N} 2 n\right)-a_{3} \cos \left(\frac{2 \pi}{N} 3 n\right) \\
\\
\displaystyle n=0,1,2 \ldots N-1.
\end{array}
$$

| *windowKind* | *a0* | *a1* | *a2* | *a3* |
| --- | --- | --- | --- | --- |
| Blackman367 | 0.42659071 | 0.49656062 | 0.07684867 | 0 |
| Blackman361 | 0.44959 | 0.49364 | 0.05677 | 0 |
| Blackman492 | 0.35875 | 0.48829 | 0.14128 | 0.01168 |
| Blackman474 | 0.40217 | 0.49703 | 0.09392 | 0.00183 |

**Cos1, Cos2, Cos3, Cos4**

$$
\begin{array}{l}
\displaystyle w(n)=\cos \left(\frac{n}{N} \pi\right)^{\alpha}, \\
\\
\displaystyle n=-\frac{N}{2}, \ldots,-1,0,1, \ldots, \frac{N}{2} .
\end{array}
$$

Cos1: *α* =1;   Cos2: *α* =2;   Cos3: *α* =3;   Cos4: *α* =4

**Hamming**

$$
w(n)=\left\{\begin{array}{ll}
\displaystyle 0.54+0.46 \cos \left(\frac{2 \pi n}{N}\right) & n=-\frac{N}{2}, \ldots,-1,0,1, \ldots, \frac{N}{2} \\
\\
\displaystyle 0.54-0.46 \cos \left(\frac{2 \pi n}{N}\right) & n=0,1,2, \ldots, N-1
\end{array}\right.
$$

**Hanning**

$$
w(n)=\left\{\begin{array}{ll}
\displaystyle \frac{1}{2}\left[1+\cos \left(\frac{2 \pi n}{N}\right)\right] & n=-\frac{N}{2}, \ldots,-1,0,1, \ldots, \frac{N}{2} \\
\\
\displaystyle \frac{1}{2}\left[1-\cos \left(\frac{2 \pi n}{N}\right)\right] & n=0,1,2, \ldots, N-1
\end{array}\right.
$$
<sub></sub>

**KaiserBessel20, KaiserBessel25,  KaiserBessel30**

$$
w(n)=\frac{\displaystyle I_{0}\left(\pi \alpha \sqrt{1-\left(\frac{2 n}{N}\right)^{2}}\right)}{I_{0}(\pi \alpha)} \quad 0 \leq|n| \leq \frac{N}{2} .
$$

*where I*<sub>0</sub> *is the zero-order modified Bessel function of the first kind.*

KaiserBessel20: *α* =2.0;   KaiserBessel25: *α* =2.5;   KaiserBessel30: *α* =3.0

**Parzen**

$$
\displaystyle w(n)=1-\left|\frac{2 n}{N}\right|^{2} \quad 0 \leq|n| \leq \frac{N}{2} .
$$

**Poisson2, Poisson3,  Poisson4**

$$
\displaystyle w(n)=\exp \left(-\alpha \frac{2|n|}{N}\right) \quad 0 \leq|n| \leq \frac{N}{2} .
$$

Poisson2: *α* =2;   Poisson3: *α* =3;   Poisson4: *α* =4

**Riemann**

$$
w(n)=\frac{\displaystyle \sin \left(\frac{2 \pi n}{N}\right)}{\left(\frac{\displaystyle 2 \pi n}{N}\right)} \quad 0 \leq|n| \leq \frac{N}{2} .
$$

**Flat-Top**

The flat-top windows are defined as a sum of cosine terms:

$$
\displaystyle w(n)=\sum_{k=0}^{m} c_{k} \cos (k z),
$$
$$
\displaystyle z=\frac{2 \pi j}{N}, \quad j=0,1, \ldots N-1 .
$$

Here are the supported flat-top window keywords for use as *windowKind* with the /WINF flag. These keywords require Igor Pro 8.00 or later:

| windowKind | Cosine Terms |
| --- | --- |
| SFT3F | c0=0.26526, c1=-0.5, c2=0.23474. |
| SFT3M | c0=0.28235, c1=-0.52105, c2=0.19659. |
| FTNI | c0=0.2810639, c1=-0.5208972, c2=0.1980399. |
| SFT4F | c0=0.21706, c1=-0.42103, c2=0.28294, c3=-0.07897. |
| SFT5F | c0=0.1881, c1=-0.36923, c2=0.28702, c3=-0.13077, c4=0.02488. |
| SFT4M | c0=0.241906, c1=-0.460841, c2=0.255381, c3=-0.041872. |
| FTHP | c0=1.0, c1=-1.912510941, c2=1.079173272, c3=-0.1832630879. |
| HFT70 | c0=1.0, c1=-1.90796, c2=1.07349, c3=-0.18199. |
| FTSRS | c0=1.0, c1=-1.93, c2=1.29, c3=-0.388, c4=0.028. |
| SFT5M | c0=0.209671, c1=-0.407331, c2=0.281225, c3=-0.092669, c4=0.0091036. |
| HFT90D | c0=1.0, c1=-1.942604, c2=1.340318, c3=-0.440811, c4=0.043097. |
| HFT95 | c0=1.0, c1=-1.9383379, c2=1.3045202, c3=-0.4028270, c4=0.0350665. |
| HFT116D | c0=1.0, c1=-1.9575375, c2=1.4780705, c3=-0.6367431, c4=0.1228389, c5=-0.0066288. |
| HFT144D | c0=1.0, c1=-1.96760033, c2=1.57983607, c3=-0.81123644, c4=0.22583558, c5=-0.02773848, c6=0.00090360. |
| HFT169D | c0=1.0, c1=-1.97441842, c2=1.65409888, c3=-0.95788186, c4=0.33673420, c5=-0.06364621, c6=0.00521942, c7=-0.00010599. |
| HFT196D | c0=1.0, c1=-1.979280420, c2=1.710288951, c3=-1.081629853, c4=0.448734314, c5=-0.112376628, c6=0.015122992, c7=-0.000871252, c8=0.000011896. |
| HFT223D | c0=1.0, c1=-1.98298997309, c2=1.75556083063, c3=-1.19037717712, c4=0.56155440797, c5=-0.17296769663, c6=0.03233247087, c7=-0.00324954578, c8=0.00013801040, c9=-0.0000013275. |
| HFT248D | c0=1.0, c1=-1.985844164102, c2=1.791176438506, c3=-1.282075284005, c4=0.667777530266, c5=-0.240160796576, c6=0.056656381764, c7=-0.008134974479, c8=0.000624544650, c9=-0.000019808998, c10=0.000000132974. |

### *References* {#references}
For more information about the use of window functions see:

Harris, F.J., "On the use of windows for harmonic analysis with the discrete Fourier Transform", *Proc, IEEE*, *66*, 51-83, 1978.

Heinzel, G., Rüdiger, A., & Schilling, R. (2002). "Spectrum and spectral density estimation by the Discrete Fourier transform (DFT), including a comprehensive list of window functions and some new at-top windows", [http://hdl.handle.net/11858/00-001M-0000-0013-557A-5](http://hdl.handle.net/11858/00-001M-0000-0013-557A-5).

### *See Also* {#see-also}
[Fourier Transforms](/igorpro/analysis/signal-processing.md#fourier-transforms) for an example that compares the FFT result with the continuous Fourier transform values.

[IFFT](/igorpro/commands/ifft.md), [DWT](/igorpro/commands/dwt.md), [CWT](/igorpro/commands/cwt.md), [STFT](/igorpro/commands/stft.md), [HilbertTransform](/igorpro/commands/hilberttransform.md), [WignerTransform](/igorpro/commands/wignertransform.md), [DSPPeriodogram](/igorpro/commands/dspperiodogram.md), [LombPeriodogram](/igorpro/commands/lombperiodogram.md), [Unwrap](/igorpro/commands/unwrap.md), [MatrixOp](/igorpro/commands/matrixop.md)

### *Demos* {#demos}
[Open FFTSwappingDemo.pxp](#igor-pxp/Examples/Analysis/FFTSwappingDemo.pxp)

[Open PSD Demo](#igor-pxp/Examples/Analysis/PSD__Demo.pxp)