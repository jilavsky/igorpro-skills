---
description: "The CWT operation computes the continuous wavelet transform (CWT) of a 1D real-valued input wave (srcWave). The input can be of any numeric type."
slug: /commands/cwt
---

<div className="command-signature">

## <strong>CWT</strong>  [ <em>flags</em> ] <em>srcWave</em> {#cwt}

</div>

The CWT operation computes the continuous wavelet transform (CWT) of a 1D real-valued input wave (*srcWave* ). The input can be of any numeric type. The computed CWT is stored in the wave M_CWT in the current data folder. M_CWT is a double precision 2D wave which, depending on your choice of mother wavelet and output format, may also be complex. The dimensionality of M_CWT is determined by the specifications of offsets and scales. The operation sets the variable V_flag to zero if successful or to a nonzero number if it fails for any reason.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> | Specifies the main output wave created by the the operation (replacing M_CWT). |
| <span class="table-cell-nowrap">/DSTS = *destSWave*</span> | Specifies the scaling output wave created by the the operation (replacing W_CWTScaling). |
|  | It is an error to specify the same wave as both *srcWave* and a destination wave. |
|  | When used in a function, the CWT operation creates real wave references for *destWave* and *destSWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/ENDM = *method*</span> | Selects the method used to handle the two ends of the data array with  direct integration (/M=1). |
|  |<table class="nested-table"><tbody><tr><td>*method*=0:</td><td>Array padded on both sides by zeros.</td></tr><tr><td>*method*=1:</td><td>Array reflected at both the start and end.</td></tr><tr><td>*method*=2:</td><td>Array entered with cyclical repetition.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* and/or *destSWave* as a free waves. |
|  | /FREE is allowed only in functions and only if *destWave* and *destSWave*, as specified by /DEST and /DSTS, are simple names or wave references structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FSCL</span> | Use correction factor to the wave scaling of the second dimension of the output wave so that the numbers are more closely related to Fourier wavelength. See reference below for more information on the calculation of these correction factors. This flag does not affect the output from the Haar wavelet. |
| <span class="table-cell-nowrap">/M = *method*</span> | Specifies the CWT computation method. |
|  |<table class="nested-table"><tbody><tr><td>*method*&nbsp;=0:</td><td>Fast method uses FFT (default).</td></tr><tr><td>*method*&nbsp;=1:</td><td>Slower method using direct integration.</td></tr></tbody></table>
|  | You should mostly use the more efficient FFT method. The direct method should be reserved to situations where the FFT is not producing optimal results. Theoretically, when the FFT method fails, the direct method should also be fairly inaccurate, e.g., in the case of undersampled signal. The main advantage in the direct method is that you can use it to investigate edge effects. |
| <span class="table-cell-nowrap">/OSCW</span> | CWT creates an output scaling wave named W_CWTScaling that can be used as the Y wave in an image plot. For example: |
|  | <code class="igor">Display; AppendImage M_CWT vs {\*,W_CWTScaling}</code> |
|  | If you omit /OSCW, CWT creates W_CWTScaling only if you include /SMP2=4. |
|  | /OSCW was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/OUT = *format*</span> | Determines the format of the output wave M_CWT. |
|  |<table class="nested-table"><tbody><tr><td>***format***</td><td>**M_CWT Format**</td></tr><tr><td>1</td><td>complex</td></tr><tr><td>2</td><td>real valued</td></tr><tr><td>4</td><td>real and contains the magnitude</td></tr></tbody></table>
|  | Depending on the method of calculation and the choice of mother wavelet, the "native" output of the transform may be real or complex. You can force the output to have a desired format using this flag. |
| <span class="table-cell-nowrap">/Q</span> | Quiet mode; no results printed to the history. |
| <span class="table-cell-nowrap">/R1 = {*startOffset*, *delta1*, *numOffsets* }</span> |  |
|  | Specifies offsets for the CWT. Offsets are the first dimension in a CWT. Normally you will calculate the CWT for the full range of offsets implied by *srcWave*  so you will not need to use this flag. However, when using the slow method, this flag restricts the output range of offsets and save some computation time. *StartOffset* (integer) is the point number of the first offset in srcWave. *delta1* is the interval between two consecutive CWT offsets. It is expressed in terms of the number *srcWave*  points. *NumOffsets* is the number of offsets for which the CWT is computed. |
|  | By default *startOffset*=0, *delta1*=1 and *numOffsets* is the number of points in *srcWave*. If you want to specify just the *startOffset*  and *delta1*, you can set *numOffsets*=0 to use the same number of points as the source wave. |
| <span class="table-cell-nowrap">/R2 = {*startScale*, *scaleStepSize*, *numScales* }</span> |  |
|  | Specifies the range of scales for the CWT is computation. Scales are the second dimension in the output wave. Note however that there are limitations on the minimum and maximum scales having to do with the sampling of your data. Because there is a rough correspondence between a Fourier spatial frequency and CWT scale it should be understood that there is also a maximum theoretical scale. This is obvious if you compute the CWT using an FFT but it also applies to the slow method. If you specify a range outside the allowed limits, the corresponding CWT values are set to NaN. |
|  | Use NaN if you want to use the default value for any parameter for this flag. |
|  | The default value for *startScale* is determined by sampling of the source wave and the wavelet parameter or order. |
|  | At a minimum you must specify either *scaleStepSize* or *numScales*. |
| <span class="table-cell-nowrap">/SMP1 = *offsetMode*</span> |  |
|  | Determines computation of consecutive offsets. Currently supporting only *offsetMode* =1 for linear, user-provided partial offset limits (see /R1 flag): *val1 = startOffset + numOffsets \* delta1*. |
| <span class="table-cell-nowrap">/SMP2 = *scaleMode*</span> |  |
|  | Determines computation of consecutive scales. *scaleMode* is 1 by default if you specify the /R2 flag. |
|  |<table class="nested-table"><tbody><tr><td>*scaleMode*=1:</td><td>Linear:</td></tr><tr><td></td><td>&lt;code class=&quot;igor&quot;&gt;theScale = startScale + index *scaleStepSize&lt;/code&gt;</td></tr><tr><td>*scaleMode*=2:</td><td>Auto:</td></tr><tr><td></td><td>&lt;code class=&quot;igor&quot;&gt;theScale = numScales * startScale/(index+1)&lt;/code&gt;</td></tr><tr><td>*scaleMode*=4:</td><td>Power of 2 scaling interval:</td></tr><tr><td></td><td>&lt;code class=&quot;igor&quot;&gt;theScale = startScale * 2.^(index *scaleStepSize)&lt;/code&gt;</td></tr></tbody></table>
|  | When using *scaleMode* =4 the operation saves the consecutive scale values in the wave W_CWTScaling. Note also that if you use *scaleMode* =4 without specifying a corresponding /R2 flag, the default *scaleStepSize* of 1 and 64 scale values gives rise to scale values that quickly exceed the allowed limits. |
|  | (See /R2 flag for more information about the different parameters used in the equations above.) |
| <span class="table-cell-nowrap">/SUBM</span> | Subtracts the mean of the input before computing the transform. /SUBM was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/SW2 = *sWave*</span> | Provides specific scale values at which the transform is evaluated. Use instead of /R2 flag. It is your responsibility to make sure that the entries in the wave are appropriate for the sampling density of *srcWave*. |
| <span class="table-cell-nowrap">/WBI1 = {*Wavelet* [, *order* ]}</span> |  |
|  | Specifies the built-in wavelet (mother) function. *Wavelet* is the name of the mother wavelet: Morlet (default), MorletC (complex), Haar, MexHat, DOG, and Paul. |
|  |<table class="nested-table"><tbody><tr><td>Morlet:</td><td>$$ \displaystyle \Psi_{0}(x)=\frac{1}{\pi^{1 / 4}} \cos (\omega x) \exp \left(-\frac{x^{2}}{2}\right) . $$</td></tr></tbody></table>
|  | By default, ω=5. Use the /WPR1 flag to specify other values for ω. |
|  |<table class="nested-table"><tbody><tr><td>MorletC:</td><td>$$ \displaystyle \Psi_{0}(x)=\frac{1}{\pi^{1 / 4}} \exp (i \omega x) \exp \left(-\frac{x^{2}}{2}\right) . $$</td></tr></tbody></table>
|  | By default, ω=5. Use the /WPR1 flag to specify other values for ω. |
|  |<table class="nested-table"><tbody><tr><td>Haar:</td><td>$$ \displaystyle \Psi_{0}(x)=\left\{\begin{array}{cc} 1 & 0 \leq x<0.5 \\ \\ -1 & 0.5 \leq x<1 \end{array} .\right. $$</td></tr><tr><td>DOG:</td><td>$$ \displaystyle \Psi_{0}(x)=\frac{(-1)^{m+1}}{\sqrt{\Gamma\left(m+\frac{1}{2}\right)}} \frac{d^{m}}{d x^{m}}\left(\exp \left(-\frac{x^{2}}{2}\right)\right) . $$</td></tr><tr><td>MexHat:</td><td>Special case of DOG with *m* =2.</td></tr><tr><td>Paul:</td><td>$$ \displaystyle \Psi_{0}(m, x)=\frac{2^{m} i^{m} m!}{\sqrt{\pi(2 m)!}}(1-i x)^{-(m+1)}. $$</td></tr></tbody></table>
|  | *order*  applies to DOG and Paul wavelets only and specifies *m*, the particular member of the wavelet family. |
|  | The default wavelet is the Morlet. |
| <span class="table-cell-nowrap">/WPR1 = {*param1* }</span> |  |
|  | *param1*  is a wavelet-specific parameter for the wavelet function selected by /WBI1. For example, use /WPR1={6} to change the Morlet frequency from the default (5). |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. If an error occurs, sets V_flag to -1 but does not halt function execution. |

### *Details* {#details}
The CWT can be computed directly from its defining integral or by taking advantage of the fact that the integral represents a convolution which in turn can be calculated efficiently using the fast Fourier transform (FFT).

When using the FFT method one encounters the typical sampling problems and edge effects. Edge effects are also evident when using the slow method but they only significant in high scales.

From sampling considerations it can be shown that the maximum frequency of a discrete input signal is 1/2dt where dt is the time interval between two samples. It follows that the smallest CWT scale is 2dt and the largest scale is Ndt where N is the total number of samples in the input wave.

The transform in M_CWT is saved with the wave scaling. *startOffset* and *delta1* are used for the X-scaling. Both *startOffset* and *delta1* are either specified by the /R1 flag or copied from *srcWave*. The Y-scaling of M_CWT depends on your choice of /SMP2. If the CWT scaling is linear then the wave scaling is based on *startScale* and *scaleStepSize*. If you are using power of 2 scaling interval then the Y wave scaling of M_CWT has a *start* =0 and *delta* =1 and the wave W_CWTScaling contains the actual scale values for each column of M_CWT. Note that W_CWTScaling has one extra data point to make it suitable for display using an operation like:


```igor
AppendImage M_CWT vs {*, W_CWTScaling}
```

We have encountered two different definitions for the Morlet wavelet in the literature. The first is a complex function and the second is real. Instead of choosing one of these definitions we implemented both so you may choose the appropriate wavelet.

### *References* {#references}
Torrence, C., and G.P. Compo, A Practical Guide to Wavelet Analysis, *Bulletin of the American Meteorological Society*,*79*, 61-78, 1998.

The Torrence and Compo journal article is also online at: [http://paos.colorado.edu/research/wavelets/](http://paos.colorado.edu/research/wavelets/).

### *See Also* {#see-also}
For discrete wavelet transforms use the [DWT](/igorpro/commands/dwt.md) operation. The [FFT](/igorpro/commands/fft.md) operation.

### *Demos* {#demos}
[Open CWT Demo](#igor-pxp/Examples/Analysis/CWT__Demo.pxp)