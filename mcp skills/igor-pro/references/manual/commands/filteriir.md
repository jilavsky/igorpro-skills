---
description: "The FilterIIR operation applies to each waveName either the automatically-designed IIR filter coefficients or the IIR filter coefficients in coefsWaveName."
slug: /commands/filteriir
---

<div className="command-signature">

## <strong>FilterIIR</strong>  [/CASC /COEF[=<em>coefsWaveName</em>] /DIM=<em>d</em> /ENDV=<em>ev</em> /HI=<em>fHigh</em>  /LO=<em>fLow</em> /N={<em>fNotch</em>, <em>notchQ</em> } /ORD=<em>order</em> /Z=<em>z</em> /ZP] [<em>waveName</em> , ... ] {#filteriir}

</div>

The FilterIIR operation applies to each *waveName* either the automatically-designed IIR filter coefficients or the IIR filter coefficients in *coefsWaveName*. Multiple filter designs are combined into a composite filter. The filter can be optionally placed into the first waveName or just used to filter the data in *waveName*.

The automatically-designed filter coefficients are bilinear transforms of the Butterworth analog prototype with an optional variable-width notch filter.

To design more advanced IIR filters, see the ***Designing the IIR Coefficients*** section below.

### *Parameters* {#parameters}
*waveName* may be multidimensional, but only the one dimension selected by /DIM is filtered. (For two-dimensional filtering, see the [MatrixFilter](/igorpro/commands/matrixfilter.md) operation.)

*waveName* may be omitted for the purpose of checking the format of *coefsWaveName*. If the format is detectably incorrect an error code will be returned in V_flag. Use /Z to prevent command execution from stopping.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/CASC</span> | Specifies that coefsWaveName contains cascaded bi-quad filter coefficients. The cascade implementation is more stable and numerically accurate for high-order IIR filtering than Direct Form 1 filtering. See ***Cascade Details*** below. |
| <span class="table-cell-nowrap">/COEF [ = *coefsWaveName* ]</span> |  |
|  | Replaces the first output *waveName* by the filter coefficients instead of the filtered results or, when *coefsWaveName* is specified, replaces the output wave(s) by the result of filtering *waveName* with the IIR coefficients in *coefsWaveName*. |
|  | *coefsWaveName* must not be one of the destination *waveNames*. It must be single- or double-precision numeric and two-dimensional. |
|  | When used with /CASC, *coefsWaveName* must have 6 columns, containing real-valued coefficients for a product of ratios of second-order polynomials (cascaded bi-quad sections). |
|  | If /ZP is specified, it must be complex, otherwise it must be real. |
|  | See ***Details*** for the format of the coefficients in *coefsWaveName*. |
| <span class="table-cell-nowrap">/DIM = *d*</span> | Specifies the wave dimension to filter. |
|  |<table class="nested-table"><tbody><tr><td>*d*&nbsp;=-1:</td><td>Treats entire wave as 1D (default).</td></tr><tr><td>*d*&nbsp;&gt;=0:</td><td>Operates along rows, columns, etc.</td></tr></tbody></table>
|  | Use /DIM=0 to apply the filter to each individual column (each one a channel, say left and right) in a multidimensional waveName where each row comprises all the sound samples at a particular time. |
| <span class="table-cell-nowrap">/ENDV = *ev*</span> | Values before the beginning of each filtered wave are replaced with *ev*. If you omit /ENDV they are replaced with zeros. To prevent filter startup artifacts set *ev* to the first value or a localized mean value at the start of the wave to be filtered. |
|  | /ENDV was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/HI = *fHigh*</span> | Creates a high-pass Butterworth filter with the -3dB corner at *fHigh*. The order of the filter is controlled by the /ORD flag. |
|  | *fHigh* is a filter design frequency measured in fractions of the sampling frequency, and may not exceed 0.5 (the normalized Nyquist frequency). |
| <span class="table-cell-nowrap">/LO = *fLow*</span> | Creates a low-pass Butterworth filter with the -3dB corner at *fLow*. The /ORD flag controls the order of the filter. |
|  | *fLow* is a filter design frequency measured in fractions of the sampling frequency, and may not exceed 0.5 (the normalized Nyquist frequency). |
|  | Create bandpass and bandreject filters by specifying both /HI and /LO. For a bandpass filter, set *fLow* > *fHigh*, and for a band reject filter, set *fLow* < *fHigh*. |
| <span class="table-cell-nowrap">/N = {*fNotch*, *notchQ*}</span> | Creates a notch filter with the center frequency at *fNotch*, and a -3dB width of *fNotch* /*notchQ*.. |
|  | *fNotch* is a filter design frequency measured in fractions of the sampling frequency, and may not exceed 0.5 (the normalized Nyquist frequency). |
|  | *notchQ* is a number greater than 1, typically 10 to 100. Large values produce a filter that "rings" a lot. |
| <span class="table-cell-nowrap">/ORD = *order*</span> | Sets the order of the Butterworth filter(s) created by /HI and /LO. The default is 2 (second order), and the maximum is 100.  When both /HI and /LO are specified, an odd value for *order* is increased to the next even number because the lowpass and highpass filters are each created with order/2. |
| <span class="table-cell-nowrap">/Z = *z*</span> | Prevents procedure execution from aborting if an error occurs. Use /Z=1 if you want to handle this case in your procedures using [GetRTError](/igorpro/commands/getrterror.md)(1) rather than having execution abort. /Z=0 is the same as no /Z at all. |
| <span class="table-cell-nowrap">/ZP</span> | Specifies that *coefsWaveName* contains complex z-domain zeros (in column 0) and poles (in column 1) or, if *coefsWaveName* is not specified, that the first output *waveName* is to be replaced by filter coefficients in the zero-pole format. See ***Zeros and Poles Details*** below. |

### *Details* {#details}
FilterIIR sets V_flag to 0 on success or to an error code if an error occurred. Command execution stops if an error occurs unless the /Z flag is set. Omit /Z and call [GetRTError](/igorpro/commands/getrterror.md) and [GetRTErrMessage](/igorpro/commands/getrterrmessage.md) under similar circumstances to see what the error code means.

### *Direct Form 1 Details* {#direct-form-1-details}
Unless /CASC or /ZP are specified, the coefficients in *coefsWaveName* describe a ratio of two polynomials of the Z transform:

<img src="Images/FilterIIR/FilterIIR_0.png" width="100%"/>

where *x* is the input wave *waveName* and *y* is the output wave (either *waveName* again or *destWaveName*).

FilterIIR computes the filtered result using the Direct Form I implementation of H(z).

The rational polynomial numerator (*a*<sub>i</sub>) coefficients in are column 0 and denominator (*b*<sub>i</sub>) coefficients in column 1 of *coefsWaveName.*

The coefficients in row 0 are the nondelayed coefficients *a*<sub>0</sub> (in column 0) and *b*<sub>0</sub> (in column 1).

The coefficients in row 1 are the *z*<sup>-1</sup> coefficients, *a*<sub>1</sub> and *b*<sub>1</sub>.

The coefficients in row n are the *z*<sup>-n</sup> coefficients, *a*<sub>n</sub> and *b*<sub>n</sub>.

The number of coefficients for the numerator can differ from the number of coefficients for the denominator. In this case, specify 0 for unused coefficients.

:::note
If all the coefficients of the denominator are 0 (*b*<sub>i</sub>= 0 except *b*<sub>0</sub> = 1), then the filter is actually a causal FIR filter (Finite Impulse Response filter with delay of *n*-1). In this sense, FilterIIR implements a superset of the [FilterFIR](/igorpro/commands/filterfir.md) operation.
:::

:::warning
**Alternate Notation**: The designation of *a*<sub>i</sub>, etc. as the numerator is at odds with many textbooks such as *Digital Signal Processing* by Oppenheim and Shafer, which uses *b* for the numerator coefficients of the rational function, *a* for the denominator coefficients with an implicit *a*<sub>0</sub> = 1, in addition to reversing the signs of the remaining denominator coefficients so that they can write H(z) as:
:::

$$
H(z)=\frac{Y(z)}{X(z)}=\frac{\displaystyle \sum_{i=0}^{n} b_{i} z^{-i}}{1-\displaystyle \sum_{i=1}^{n} a_{i} z^{-i}} .
$$

Coefficients derived using this notation need their denominator coefficients sign-reversed before putting them into rows 1 through N of column 1 (the *second* column), and the "missing" nondelayed denominator coefficient of 1.0 placed in row 0, column 1.

### *Cascade Details* {#cascade-details}
When using /CASC, the coefficients in *coefsWaveName* describe the product of one or more ratios of two quadratic polynomials of the Z transform:

$$
\displaystyle H(z)=\frac{Y(z)}{X(z)}=\prod_{k=1}^{K} \frac{a_{0_{k}}+a_{1_{k}} z^{-1}+a_{2_{k}} z^{-2}}{b_{0_{k}}+b_{1_{k}} z^{-1}+b_{2_{k}} z^{-2}} .
$$

Each product term implements a "cascaded bi-quad section", and H(z) can be realized by feeding the output of one section to the next one.

The cascade coefficients filter the data using a Direct Form II cascade implementation:

<img src="Images/FilterIIR/FilterIIR_3.png" width="100%"/>

The cascade implementation is more stable and numerically accurate for high-order IIR filtering than Direct Form I filtering. Cascade IIR filtering is recommended when the filter order exceeds 16 (a 16th-order Direct Form I filter has 17 numerator coefficients and 17 denominator coefficients).

*coefsWaveName* must be a six-column real-valued numeric wave. Each row describes one bi-quad section. The coefficients are arranged thusly:

The coefficients for the second term (or "section") of the product (*k* =2) are in the following row, etc:


| k | Row | Col 0 | Col 1 | Col 2 | Col 3 | Col 4 | Col 5 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 0 | a<sub>0</sub><sub>1</sub> | a<sub>1</sub><sub>1</sub> | a<sub>2</sub><sub>1</sub> | b<sub>0</sub><sub>1</sub> | b<sub>1</sub><sub>1</sub> | b<sub>2</sub><sub>1</sub> |
| 2 | 1 | a<sub>0</sub><sub>2</sub> | a<sub>1</sub><sub>2</sub> | a<sub>2</sub><sub>2</sub> | b<sub>0</sub><sub>2</sub> | b<sub>1</sub><sub>2</sub> | b<sub>2</sub><sub>2</sub> |
|  | ... |  |  |  |  |  |  |

The number of coefficients for the numerator (*a* 's) is allowed to differ from the number of coefficients for the denominator (*b* 's). In this case, specify 0 for unused coefficients.

For example, a third order filter (three poles and three zeros) cascade implementation is a single-order section combined with a second order section. The values for *a*<sub>2</sub><sub>k</sub>, *b*<sub>2</sub><sub>k</sub> for that section (*k*) would be 0. Here the second section is specified as the first-order section:


| k | Row | Col 0 | Col 1 | Col 2 | Col 3 | Col 4 | Col 5 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 0 | a<sub>0</sub><sub>1</sub> | a<sub>1</sub><sub>1</sub> | a<sub>2</sub><sub>1</sub> | b<sub>0</sub><sub>1</sub> | b<sub>1</sub><sub>1</sub> | b<sub>2</sub><sub>1</sub> |
| 2 | 1 | a<sub>0</sub><sub>2</sub> | a<sub>1</sub><sub>2</sub> | 0 | b<sub>0</sub><sub>2</sub> | b<sub>1</sub><sub>2</sub> | 0 |

:::warning
**Alternate Notation:** In the DSP literature, the *b*<sub>0</sub><sub>k</sub> values are typically set to 1 and the H(z) expression contains an overall gain value, usually "K". Here each product term (or "section") has a user-settable gain value (*b*<sub>0</sub><sub>k</sub>). Computing the correct gain values to control overflow in integer implementations is the responsibility of the user. For floating implementations, you might as well set all *b*<sub>0</sub><sub>k</sub> values to 1 except, say, *b*<sub>0</sub><sub>1</sub>, to control the overall gain.
:::

### *Zeros and Poles Details* {#zeros-and-poles-details}
When using /ZP, coefficients in *coefsWaveName* contains **complex** zeros and poles in the (also complex) Z transform domain:

$$
\displaystyle H(z)=\frac{Y(z)}{X(z)}=\frac{\left(z-z_{0}\right)\left(z-z_{1}\right)\left(z-z_{2}\right) \ldots}{\left(z-p_{0}\right)\left(z-p_{1}\right)\left(z-p_{2}\right) \ldots}
$$

*coefsWaveName* must be a two-column complex wave with zero0, zero1, ... zeroN in the first column of N+1 rows, and pole0, pole1,... poleN in the second column of those same rows:


| k | Row | Col 0 | Col 1 |
| --- | --- | --- | --- |
| 1 | 0 | (zero0Real, zero0Imag) | (pole0Real, pole0Imag) |
| 2 | 1 | (zero1Real, zero1Imag) | (pole1Real, pole1Imag) |
| 3 | 2 | (zero2Real, zero2Imag) | (pole2Real, pole2Imag) |
|  | ... |  |  |

If a zero or pole has a nonzero imaginary component, the conjugate zero or pole must be included in *coefsWaveName*. For example, if a zero is placed at (0.7, 0.5), the conjugate is (0.7, -0.5), and that value must also appear in column 0. These two zeros form what is known as a "conjugate pair". The conjugate values must match within the greater of 1.0e-6 or 1.0e-6 * |zeroOrPole|.

Use (0,0) for unused poles or zeros, as a zero or pole at *z* = (0,0) has no effect on the filter frequency response.

The /ZP format for the coefficients is internally converted into the Direct Form 1 implementation, or into the Cascade Direct Form 2 implementation if /CASC is specified. There is no option for returning these implementation-dependent coefficients in a wave.

### *Designing the IIR Coefficients* {#designing-the-iir-coefficients}
Simple IIR filters can be used or created by specifying the /LO, /HI, /ORD, /N, /CASC, and /ZP flags. Use /COEF without *coefsWaveName* to put these simple IIR filter coefficients into the first *waveName*.

More advanced IIR filters (Bessel, Chebyshev) can be designed using the separate [Igor Filter Design Laboratory (IFDL)](/igorpro/analysis/igor-filter-design-laboratory.md). IFDL is an Igor package that you use to design FIR (Finite Impulse Response) and IIR (Infinite Impulse Response) filters and to apply them to your data. The IIR design software creates IIR coefficients based on bilinear transforms of analog prototype filters such as Bessel, Butterworth, and Chebyshev.

Even without IFDL, you can create custom IIR filters by manually placing poles and zeros in the Z plane using the Pole and Zero Filter Design procedures. Copy the following line to your Procedure window and click the Compile button at the bottom of the procedure window:


```igor
#include <Pole And Zero Filter Design>
```

Then choose "Pole and Zero Filter Design" from the Analysis menu.

### *Examples* {#examples}

```igor
// Make test sound from three sine waves
Variable/G fs= 44100                        // sampling frequency
Variable/G seconds= 0.5                     // duration
Variable/G n= 2*round(seconds*fs/2)
Make/O/W/N=(n) sound                        // 16-bit integer sound wave
SetScale/p x, 0, 1/fs, "s", sound
Variable/G f1= 200, f2= 1000, f3= 7000
Variable/G a1=100, a2=3000,a3=1500 
sound= a1*sin(2*pi*f1*x)
sound += a2*sin(2*pi*f2*x)
sound += a3*sin(2*pi*f3*x)+gnoise(10)       // add a noise floor

// Compute the sound's spectrum in dB
FFT/MAG/WINF=Hanning/DEST=soundMag sound
soundMag= 20*log(soundMag)
SetScale d, 0, 0, "dB", soundMag

// Apply a 5 kHz, 6th order low-pass filter to the sound wave
Duplicate/O sound, soundFiltered
FilterIIR/LO=(5000/fs)/ORD=6 soundFiltered	// second order by default

// Compute the filtered sound's spectrum in dB
FFT/MAG/WINF=Hanning/DEST=soundFilteredMag soundFiltered
soundFilteredMag= 20*log(soundFilteredMag)
SetScale d, 0, 0, "dB", soundFilteredMag

// Compute the filter's frequency and phase by filtering an impulse
Make/O/D/N=2048 impulse= p==0               // impulse at t==0
SetScale/P x, 0, 1/fs, "s", impulse
Duplicate/O impulse, impulseFiltered
FilterIIR/LO=(5000/fs)/ORD=6 impulseFiltered
FFT/MAG/DEST=impulseMag impulseFiltered
impulseMag= 20*log(impulseMag)
SetScale d, 0, 0, "dB", impulseMag
FFT/OUT=5/DEST=impulsePhase impulseFiltered
impulsePhase *= 180/pi                      // convert to degrees
SetScale d, 0, 0, "deg", impulsePhase
Unwrap 360, impulsePhase                    // continuous phase

// Graph the frequency responses
Display/R/T impulseMag as "IIR Lowpass Example"
AppendToGraph/L=phase/T impulsePhase
AppendToGraph soundMag, soundFilteredMag
ModifyGraph axisEnab(left)={0,0.6}
ModifyGraph axisEnab(right)={0.65,1}
ModifyGraph axisEnab(phase)={0.65,1}
ModifyGraph freePos=0, lblPos=60, rgb(soundFilteredMag)=(0,0,65535)
ModifyGraph rgb(impulseMag)=(0,0,0), rgb(impulsePhase)=(0,65535,0)
ModifyGraph axRGB(phase)=(3,52428,1), tlblRGB(phase)=(3,52428,1)
Legend
```

<img src="Images/FilterIIR/FilterIIR_6.png" width="100%"/>


```igor
// Graph the unfiltered and filtered impulse time responses
Display/L=leftImpulse impulse as "IIR Filtered Impulse"
AppendToGraph/L=leftFiltered impulseFiltered
ModifyGraph axisEnab(leftImpulse)={0,0.45}, axisEnab(leftFiltered)={0.55,1}
ModifyGraph freePos=0, margin(left)=50
ModifyGraph mode(impulse)=1, rgb(impulseFiltered)=(0,0,65535)
SetAxis bottom -0.00005,0.001
Legend
```

<img src="Images/FilterIIR/FilterIIR_8.png" width="100%"/>


```igor
// Listen to the sounds
PlaySound sound         // this has a very high frequency tone
PlaySound soundFiltered // this doesn't
```

### *References* {#references}
Embree, P.M., and B. Kimble, *C Language Algorithms for Signal Processing*, 456 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1991.

Lynn, P.A., and W. Fuerst, *Introductory Digital Signal Processing with Computer Applications*, 479 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1998.

Oppenheim, A.V., and R.W. Schafer, *Digital Signal Processing*, 585 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1975.

Terrell, T.J., *Introduction to Digital Filters*, 2nd ed., 261 pp., John Wiley & Sons, New York, 1988.

### *See Also* {#see-also}
[Smoothing](/igorpro/analysis/signal-processing.md#smoothing), [FilterFIR](/igorpro/commands/filterfir.md), [FFT](/igorpro/commands/fft.md), [IIR Filters](/igorpro/analysis/signal-processing.md#iir-filters)