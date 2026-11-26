---
description: "The Correlate operation correlates srcWaveName with each destination wave, putting the result of each correlation in the corresponding destination wave."
slug: /commands/correlate
---

<div className="command-signature">

## <strong>Correlate</strong>  [/AUTO/C/NODC] <em>srcWaveName</em>, <em>destWaveName</em> [, <em>destWaveName</em> ]... {#correlate}

</div>

The Correlate operation correlates *srcWaveName* with each destination wave, putting the result of each correlation in the corresponding destination wave.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/AUTO</span> | Auto-correlation scaling. This forces the X scaling of the destination wave's center point to be x=0, and divides the destination wave by the center point's value so that the center value is exactly 1.0. |
|  | If *srcWaveName* and *destWaveName* do not have the same number of points, this flag is ignored. |
|  | /AUTO is not compatible with /C. |
| <span class="table-cell-nowrap">/C</span> | Circular correlation. (See Compatibility Note, below). Don't use /C for auto-correlation (where *srcWaveName* and *destWaveName* are the same). |
| <span class="table-cell-nowrap">/NODC</span> | Removes the mean from the source and destination waves before computing the correlations. Removing the mean results in the un-normalized auto- or cross-covariance. |
|  | "DC" is an abbrevation of "direct current", an electronics term for the non-varying average value component of a signal. |

### *Details* {#details}

:::note
To compute a single-value correlation number use the StatsCorrelation function which returns the Pearson's correlation coefficient of two same-length waves.
:::

Depending on the type of correlation, the destination waves' length may increase. *srcWaveName*  is not altered unless it also appears as a destination wave.

If the source wave is real-valued, each destination wave must be real-valued and if the source wave is complex, each destination wave must be complex, too. Double and single precision waves may be freely intermixed; the calculations are performed in the higher precision.

The linear correlation equation is:

$$
\displaystyle {destWaveOut}[p]=\sum_{m=0}^{N-1} {srcWave}[m] \cdot {destWaveIn}[p+m]
$$

where *N*  is the number of points in the longer of *destWaveIn*  and *srcWave*.

For circular correlation, the index [*p* +*m* ] is wrapped around when it exceeds the range of [0,numpnts(*destWaveIn* )-1]. For linear correlation, when *p* +*m*  exceeds the range a zero value is substituted for *destWaveIn* [*p* +*m* ]. When *m* exceeds numpnts(*srcWave* )-1, 0 is used instead of *srcWave* [*m*].

Comparing this with the [Convolve](/igorpro/commands/convolve.md) operation whose linear convolution equation is:

$$
\displaystyle {destWaveOut}[p]=\sum_{m=0}^{N-1} {destWaveIn}[m] \cdot {srcWave}[p-m]
$$

you can see that the main difference is that for correlation the source wave is not reversed before shifting and combining with the destination wave.

The Correlate operation is not multidimensional aware.  See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

### *Compatibility Note* {#compatibility-note}
Prior to Igor Pro 5, Correlate/C scaled and rotated the results improperly (the result was often rotated left by one and the X scaling was entirely negative).

Now the destination wave's X scaling is unaltered and it does not rotate the result. You can force the old behavior for compatibility with old procedures that depend on the old behavior by setting root:V_oldCorrelationScaling=1.

A better way to get identical Correlate/C results with all versions of Igor Pro is to use this code, which rotates the result so that x=0 is always the first point in *destWave*, no matter which Igor Pro version runs this code (currently, it doesn't change anything and runs extremely quickly because it does no rotation):


```igor
Correlate/C srcWave, destWave
Variable pointAtXEqualZero= x2pnt(destWave,0)	// 0 for Igor Pro 5
Rotate -pointAtXEqualZero,destWave
SetScale/P x, 0, DimDelta(destWave,0), "", destWave
```

### *Applications* {#applications}
A common application of correlation is to measure the similarity of two input signals as they are shifted by one another.

Often it is desirable to normalize the correlation result to 1.0 at the maximum value where the two inputs are most similar. To normalize *destWaveOut*, compute the RMS values of the input waves and the number of points in each wave:


```igor
WaveStats/Q srcWave
Variable srcRMS= V_rms
Variable srcLen= numpnts(srcWave)	

WaveStats/Q destWave
Variable destRMS= V_rms
Variable destLen= numpnts(destWave)	

Correlate srcWave, destWave	// overwrites destWave

// now normalize to max of 1.0
destWave /= (srcRMS * sqrt(srcLen) * destRMS * sqrt(destLen))
```

Another common application is using autocorrelation (where *srcWaveName* and *destWaveName* are the same) to determine Power Spectral Density. In this case it better to use the [DSPPeriodogram](/igorpro/commands/dspperiodogram.md) operation which provides more options.

### *See Also* {#see-also}
[Convolve](/igorpro/commands/convolve.md), [Correlation](/igorpro/analysis/signal-processing.md#correlation), [MatrixOp](/igorpro/commands/matrixop.md), [StatsCorrelation](/igorpro/commands/statscorrelation.md), [StatsCircularCorrelationTest](/igorpro/commands/statscircularcorrelationtest.md), [StatsLinearCorrelationTest](/igorpro/commands/statslinearcorrelationtest.md), [DSPPeriodogram](/igorpro/commands/dspperiodogram.md)

### *References* {#references}
An explanation of autocorrelation and Power Spectral Density (PSD) can be found in Chapter 12 of William H. Press, et al., *Numerical Recipes in C*, Cambridge University Press, 1988.

WaveMetrics provides Igor Technical Note 006, "DSP Support Macros" which computes the PSD with options such as windowing and segmenting. See the Technical Notes folder. Some of the techniques discussed there are available as Igor procedure files in the WaveMetrics Procedures:Analysis folder.

Wikipedia: [http://en.wikipedia.org/wiki/Correlation](http://en.wikipedia.org/wiki/Correlation)

Wikipedia: [http://en.wikipedia.org/wiki/Cross_covariance](http://en.wikipedia.org/wiki/Cross_covariance)

Wikipedia: [http://en.wikipedia.org/wiki/Autocorrelation_function](http://en.wikipedia.org/wiki/Autocorrelation_function)

### *Demos* {#demos}
[Open PSD Demo](#igor-pxp/Examples/Analysis/PSD__Demo.pxp)