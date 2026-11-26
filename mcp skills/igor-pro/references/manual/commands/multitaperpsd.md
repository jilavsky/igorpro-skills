---
description: "The MultiTaperPSD operation estimates the power spectral density of srcWave using Slepian (DPSS) tapers."
slug: /commands/multitaperpsd
---

<div className="command-signature">

## <strong>MultiTaperPSD</strong>  [<em>flags</em>] <em>srcWave</em> {#multitaperpsd}

</div>

The MultiTaperPSD operation estimates the power spectral density of *srcWave* using Slepian (DPSS) tapers.

The MultiTaperPSD operation was added in Igor Pro 7.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Uses Thomson's adaptive algorithm. In this case the operation also creates the wave W_MultiTaperDF that contains the effective degrees of freedom. For each frequency of the PSD the algorithm is expected to converge within few iterations. When it fails to converge, the operation prints in the history the total number of frequencies where it did not converge while the actual output contains the last iteration estimate. |
| <span class="table-cell-nowrap">/DB</span> | Scale the PSD results as 10\*log<sub>10</sub>(spectralEst(f)). |
| <span class="table-cell-nowrap">/DBF = *f0*</span> | Scale the PSD results as 10\*log<sub>10</sub>(spectralEst(f)/spectralEst(*f0*)) where *f0* must be in the range [0,0.5/DimDelta(srcWave,0)]. |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Saves the PSD estimate in a wave specified by *destWave*. The destination wave is created or overwritten if it already exists. |
|  | Creates a wave reference for the destination wave in a user function. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | If you omit /DEST the operation saves the resulting spectral estimate in the wave W_MultiTaperPSD in the current data folder. |
| <span class="table-cell-nowrap">/F</span> | Computes F-test statistic for each output frequency. The results are stored in the wave W_MultiTaperF. |
|  | If /DEST is also used then the F-test results are stored in the same data folder as *destWave*. Otherwise W_MultiTaperF is created in the current data folder. |
|  | The statistic is a variance ratio, of the background and the power at the specific frequency. Since the PSDs of the background and the line are assumed to be distributed as Chi-squared with 2 and 2\*nTapers-2 degrees of freedom respectively, the relevant critical value for computing confidence intervals can be obtained from: |
|  | <code class="igor">StatsInvFCdf(percentSignificance/100,2,2\*nTapers-2)</code> |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* as a free wave.  This flag does not affect any other wave created by the operation. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/NOR = *N*</span> | Sets the normalization factor that is used to multiply each element of the output. For example, if you want to normalize the output such that the sum of the PSD estimate matches the variance of the input use /NOR=2/(np*np) where np is the number of points in *srcWave*. |
| <span class="table-cell-nowrap">/NTPR = *nTapers*</span> | Specifies the number of Slepian tapers to be used. If you do not specify a number of tapers, the operation uses 2\**nw* (twice the time-bandwidth product). |
| <span class="table-cell-nowrap">/NW = *nw*</span> | Specifies the time-bandwidth product. This value should typically be in the range [2,6]. Given a time-bandwidth product *nw* it is recommended to use no more than 2\**nw* tapers in order to maximize variance efficiency. |
| <span class="table-cell-nowrap">/Q</span> | Quiet mode; suppresses printing in the history area. |
| <span class="table-cell-nowrap">/R = [*startPoint*,*endPoint*]</span> |  |
|  | Calculates the PSD estimate for a specified input range. *startPoint* and *endPoint* are expressed in terms of point numbers of the source wave. |
| <span class="table-cell-nowrap">/R = (*startX*,*endX*)</span> |  |
|  | Calculates the PSD estimate for a specified input range. *startX* and *endX* are expressed in terms of X values. Note that this option converts your X specifications to point numbers and some roundoff may occur. |
| <span class="table-cell-nowrap">/Z</span> | Do not report errors. |

### *Details* {#details}
The MultiTaperPSD operation estimates the PSD of *srcWave* by computing a set of discrete prolate spheroidal functions (Slepian [DPSS](/igorpro/commands/dpss.md)) and using them as optimal window functions. The window functions/tapers are applied to the input signal and squares of the resulting Fourier transforms are weighted together to produce the PSD estimate.

*srcWave* must be a real-valued numeric wave of single or double precision and must not contain any INFs or NaNs.

The mean value of the input is subtracted prior to multiplication by the tapers. Like [DSPPeriodogram](/igorpro/commands/dspperiodogram.md), the MultiTaperPSD operation leaves the normalization to the user.

The default PSD estimate is calculated by combining the Fourier transforms of the tapered signal with weights from the DPSS calculation. You can use the /A flag to improve the PSD estimate for increasing tapers. Thomson's adaptive algorithm is reasonably efficient and also provides an estimate of the effective degrees of freedom as a function of frequency.

The operation sets the variable V_Flag to zero if successful or to a -1 if it encounters an error. If you are using Thomson's adaptive algorithm (/A) V_Flag is set to the number of frequencies at which the algorithm failed to converge.

### *See Also* {#see-also}
[FFT](/igorpro/commands/fft.md), [DSPPeriodogram](/igorpro/commands/dspperiodogram.md), [DPSS](/igorpro/commands/dpss.md), [ImageWindow](/igorpro/commands/imagewindow.md) , [Hanning](/igorpro/commands/hanning.md), [LombPeriodogram](/igorpro/commands/lombperiodogram.md)

### *Demos* {#demos}
[Open MultiTaperPSD Demo](#igor-pxp/Examples/Analysis/MultiTaperPSD__Demo.pxp)

### *References* {#references}
D.J. Thomson: "Spectrum Estimation and Harmonic Analysis", Proc. IEEE 70 (9) 1982 pp. 1055.

D. Slepian, "Prolate Spheroidal Wave Functions, Fourier Analysis, and Uncertainty -- V: the Discrete Case", Bell System Tech J. Vol 57 (5) May-June 1978.

Lees, J. M. and J. Park (1995). Multiple-taper spectral analysis: A stand-alone C-subroutine: Computers & Geosciences: 21, 199-236.