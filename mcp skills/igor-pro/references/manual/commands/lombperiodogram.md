---
description: "The LombPeriodogram is used in spectral analysis of signal amplitudes specified by srcAmpWave which are sampled at possibly random sampling times given by…"
slug: /commands/lombperiodogram
---

<div className="command-signature">

## <strong>LombPeriodogram</strong>  [ /NF=<em>numFrequencies</em>  /DESP=<em>datafolderAndName</em>   /DEST=<em>datafolderAndName</em>  /FR=<em>frequencyResolution</em>  /Q /Z ] <em>srcTimeWave</em>, <em>srcAmpWave</em> [, <em>srcFreqWave</em> ] {#lombperiodogram}

</div>

The LombPeriodogram is used in spectral analysis of signal amplitudes specified by *srcAmpWave* which are sampled at possibly random sampling times given by *srcTimeWave* . The only assumption about the sampling times is that they are ordered from small to large time values. The periodogram is calculated for either a set of frequencies specified by *srcFreqWave* (slow method) or by the flags /FR and /NF (fast method). Unless you specify otherwise, the results of the operation are stored by default in W_LombPeriodogram and W_LombProb in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DESP = *datafolderAndName*</span> |  |
|  | Saves the computed P-values in a wave specified by *datafolderAndName*. The destination wave will be created or overwritten if it already exists. *dataFolderAndName* can include a full or partial path with the wave name. |
|  | Creates by default a wave reference for the destination wave in a user function. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | If this flag is not specified, the operation saves the P-values in the wave W_LombProb in the current data folder. |
| <span class="table-cell-nowrap">/DEST = *datafolderAndName*</span> |  |
|  | Saves the computed periodogram in a wave specified by *datafolderAndName*. The destination wave will be created or overwritten if it already exists. *dataFolderAndName* can include a full or partial path with the wave name (/DEST=root:bar:destWave). |
|  | Creates by default a wave reference for the destination wave in a user function. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | If this wave is not specified the operation saves the resulting periodogram in the wave W_LombPeriodogram in the current data folder. |
| <span class="table-cell-nowrap">/FR = *fRes*</span> | Use /FR to specify the frequency resolution of the output. This flag is used together with /NF to specify the range of frequencies for which the periodogram is computed. Note that *fRes* is also the lowest frequency in the output. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all specified destination waves as free waves. This flag does not affect  output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions and only if *datafolderAndName*, as specified by /DESP or /DEST, are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/NF = *numFreq*</span> | Use /NF to specify the number of frequencies at which the periodogram is computed. The range of frequencies of the periodogram is then [fRes, (*numFreq*-1)*fRes]. |
| <span class="table-cell-nowrap">/Q</span> | Quiet mode; suppresses printing results in the history area. |
| <span class="table-cell-nowrap">/Z</span> | Do not report any errors. |

### *Details* {#details}
The LombPeriodogram (sometimes referred to as "Lomb-Scargle" periodogram) is useful in detection of periodicities in data. The main advantage of this approach over Fourier analysis is that the data are not required to be sampled at equal intervals. For an input consisting of N points this benefit comes at a cost of an O(N<sup>2</sup>) computations which becomes prohibitive for large data sets. The operation provides the option of computing the periodogram at equally spaced (output) frequencies using /FR and /NF or at completely arbitrary set of frequencies specified by *srcFreqWave.* It turns out that when you use equally spaced output frequencies the calculation is more efficient because certain parts of the calculation can be factored.

The Lomb periodogram is given by

$$
L P(\omega)=\frac{1}{2 \sigma^{2}}\left\{\frac{\left[\displaystyle \sum_{i=0}^{N-1}\left(y_{i}-\bar{y}\right) \cos \left[\omega\left(t_{i}-\tau\right)\right]\right]^{2}}{\displaystyle \sum_{i=0}^{N-1} \cos ^{2}\left[\omega\left(t_{i}-\tau\right)\right]}+\frac{\left[\displaystyle \sum_{i=0}^{N-1}\left(y_{i}-\bar{y}\right) \sin \left[\omega\left(t_{i}-\tau\right)\right]\right]^{2}}{\displaystyle \sum_{i=0}^{N-1} \sin ^{2}\left[\omega\left(t_{i}-\tau\right)\right]}\right\}
$$

Here y<sub>i</sub> is the ith point in *srcAmpWave*, t<sub>i</sub> is the corresponding point in *srcTimeWave*,

$$
\displaystyle \sigma^{2}=\frac{1}{N-1} \sum_{i=0}^{N-1}\left(y_{i}-\bar{y}\right)^{2},
$$

and

$$
\tan (2 \omega \tau)=\frac{\displaystyle \sum_{i=0}^{N-1} \sin \left(2 \omega t_{i}\right)}{\displaystyle \sum_{i=0}^{N-1} \cos \left(2 \omega t_{i}\right)} .
$$

In the absence of a Nyquist limit, the number of independent frequencies that you can compute can be estimated using:

$$
\displaystyle N_{i n d}=-6.362+1.193 N+0.00098 N^{2} .
$$

This expression was given by Horne and Baliunas derived from least square fitting. N<sub>ind</sub> is used to compute the P-values as:

$$
\displaystyle p=1-\{1-\exp [L P(w)]\}^{N_{\text {ind }}} .
$$

:::note
You can invert the last expression to determine the value of LP(ω) for any significance level.
:::

### *See Also* {#see-also}

[FFT](/igorpro/commands/fft.md), [DSPPeriodogram](/igorpro/commands/dspperiodogram.md)

### *References* {#references}

1. J.H. Horne and S.L. Baliunas, *Astrophysical Journal*, **302**, 757-763, 1986.


2. N.R. Lomb, *Astrophysics and Space Science*, **39**, 447-462, 1976.


3. W.H. Press, B.P. Flannery, S.A. Teukolsky, and W.T. Vetterling, *Numerical Recipes*, 3rd ed., Section 13.8.