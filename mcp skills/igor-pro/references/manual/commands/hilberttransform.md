---
description: "The HilbertTransform operation computes the Hilbert transformation of srcWave, which is a real or complex (single or double precision) wave of 1-3 dimensions."
slug: /commands/hilberttransform
---

<div className="command-signature">

## <strong>HilbertTransform</strong>  [<em>flags</em>] <em>srcWave</em> {#hilberttransform}

</div>

The HilbertTransform operation computes the Hilbert transformation of *srcWave*, which is a real or complex (single or double precision) wave of 1-3 dimensions. The result of the HilbertTransform is stored in *destWave*, or in the wave W_Hilbert (1D) or M_Hilbert in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Creates a real wave reference for the destination wave in a user function. See [Automatic Creation of WAVE References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* (specified by /DEST) as a free wave. |
|  | /FREE is allowed only in functions, and only if *destWave* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/O</span> | Overwrites *srcWave*  with the transform. |
| <span class="table-cell-nowrap">/PAD = {*dim1* [, *dim2*, *dim3*, *dim4* ]}</span> |  |
|  | Converts *srcWave*  into a padded wave of dimensions *dim1*, *dim2..*. The padded wave contains the original data at the start of the dimension and adds zero entries to each dimension up to the specified dimension size. The *dim1*... values must be greater than or equal to the corresponding dimension size of *srcWave*. If you need to pad just the lowest dimension(s) you can omit the remaining dimensions; for example, /PAD=*dim1*  will set *dim2*  and above to match the dimensions in *srcWave*. |
|  | This flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The Hilbert transform of a function *f*(*x*) is defined by:

$$
\displaystyle F(t)=\frac{1}{\pi t} \int_{-\infty}^{\infty} \frac{f(x) d x}{x-t} .
$$

Theoretically, the integral is evaluated as a Cauchy principal value. Computationally one can write the Hilbert transform as the convolution:

$$
\displaystyle F(t)=\frac{-1}{\pi t} * f(t),
$$

which by the convolution theorem of Fourier transforms, may be evaluated as the product of the transform of *f*(*x*) with -*i*\*sgn(*x*) where:

$$
\displaystyle \operatorname{sgn}(x)=\left\{\begin{array}{cc}
-1 & x<0 \\
\\
0 & x=0 \\
\\
1 & x>0
\end{array} .\right.
$$

Note that the Hilbert transform of a constant is zero. If you compute the Hilbert transform in more than one dimension and one of the dimensions does not vary (is a constant), the transform will be zero (or at least numerically close to zero).

There are various definitions for the extension of the Hilbert transform to more than one dimension. In two dimensions this operation computes the transform by multiplying the 2D Fourier transform of the input by the factor (-i)sgn(x)(-i)sgn(y) and then computing the inverse Fourier Transform. A similar procedure is used when the input is 3D.

### *Examples* {#examples}
Extract the instantaneous amplitude and frequency of a narrow-band signal.


```igor
Make/O/N=1000 w0,amp,phase
SetScale/I x 0,50,"", w0,amp,phase
w0 = exp(-x/10)*cos(2*pi*x)
HilbertTransform /DEST=w0h w0   // w0+i*w0h is the "analytic signal", i=cmplx(0,1)
amp = sqrt(w0^2 + w0h^2)        // extract the envelope
phase = atan2(-w0h,w0)          // extract the phase  [SIGN CONVENTION?]
Unwrap 2*pi, phase              // eliminate the 2*pi phase jumps
Differentiate phase /D=freq     // would have less noise if fit to a line over interior points
freq /= 2*pi                    // phase = 2*pi*freq*time
Display w0,amp                  // original waveform and its envelope;  note boundary effects
Display freq                    // instantaneous frequency estimate, with boundary effects
```

Compute the envelope of a signal:


```igor
Function calcEnvelope(Wave ddd)
HilbertTransform/dest=ht ddd
Matrixop/o sEnv=abs(cmplx(ddd,ht))
CopyScales ddd,sEnv
KillWaves/z ht
End
```

### *See Also* {#see-also}
[FFT](/igorpro/commands/fft.md)

### *References* {#references}
Bracewell, R., *The Fourier Transform and Its Applications*, McGraw-Hill, 1965.