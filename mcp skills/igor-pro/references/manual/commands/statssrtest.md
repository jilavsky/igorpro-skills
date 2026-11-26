---
description: "The StatsSRTest operation performs a parametric or nonparametric serial randomness test on srcWave, which must contain finite numerical data."
slug: /commands/statssrtest
---

<div className="command-signature">

## <strong>StatsSRTest</strong>  [ /ALPH=<em>alpha</em>  /P /NAPR /NP /T=<em>k</em>  /Z /Q ] <em>srcWave</em> {#statssrtest}

</div>

The StatsSRTest operation performs a parametric or nonparametric serial randomness test on srcWave, which must contain finite numerical data. The null hypothesis of the test is that the data are randomly distributed. Output is to the W_StatsSRTest wave in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/GCD</span> | Tests the output of a random number generator (RNG). *srcWave* consists of values between 0 and 2^32 (converted to unsigned 32-bit integers). GCD computes the gcd for consecutive pairs of data in *srcWave*. The number of steps in the GCD and the distribution of the GCD's are compared with ideal distributions and corresponding P values are reported. This test is part of Marsaglia's Die-Hard battery of tests. P-values close to either 0 or 1 indicate a nonideal RNG. You should use the reported minimum and maximum values to check that the input is indeed in the proper range. Typically *srcWave* consists of at least1e6 entries. |
| <span class="table-cell-nowrap">/NAPR</span> | Use the normal approximation even when the number of points is below 150. |
| <span class="table-cell-nowrap">/NP</span> | Performs a nonparametric serial randomness test by counting the numbers of runs up and down and computing the probability that such a value is obtained by chance. |
| <span class="table-cell-nowrap">/P</span> | Performs a parametric serial randomness test. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. |

### *Details* {#details}
The parametric test for serial randomness is according to Young. *C* is given by

$$
C=1-\frac{\displaystyle \sum_{i=0}^{n-2}\left(X_{i}-X_{i+1}\right)^{2}}{\displaystyle 2 \sum_{i=0}^{n-1}\left(X_{i}-\bar{X}\right)^{2}},
$$

where 
$$
\displaystyle \bar{X}
$$
 is the mean and n is the number of points in *srcWave*. The critical value is obtained from mean square successive difference distribution [StatsInvCMSSDCDF](/igorpro/commands/statsinvcmssdcdf.md). For more than 150 points, StatsSRTest uses the normal approximation and provides the critical values from the normal distribution. For samples from a normal distribution, *C* is symmetrically distributed about 0 with positive values indicating positive correlation between successive entries and negative values corresponding to negative correlation.

The nonparametric test consists of counting the number of runs that are successive positive or successive negative differences between sequential data. If two sequential data are the same it computes two numbers of runs by considering the two possibilities where the equality is replaced with either a positive or a negative difference. The results of the operation include the number of runs up and down, the number of unchanged values (the number of places with no difference between consecutive entries), the size of the longest run and its associated probability, the number of converted equalities, and the probability that the number of runs is less than or equal to the reported number ([StatsRunsCDF](/igorpro/commands/statsrunscdf.md)). When equalities are encountered the operation computes the probabilities that the computed number of runs or less can be found in an equivalent random sequence.

Converted equalities are those with the same sign on both sides so that when we replace the equality by the opposite sign we increase the number of runs. The equalities that are not converted are found between two different signs and therefore regardless of the sign that we give them they do not affect the total number of runs. We implicitly assume that the data does not contain more than one sequential equalities.

The longest run is determined without taking into account equalities or their conversions. The probability of the longest run is computed from Equation 6 of Olmstead, which is accurate within 0.001 when the number of runs is 5 or more. This probability applies to either positive or negative differences and should be divided by two if a specific sign is selected.

### *References* {#references}
Bradley, J.V., *Distribution-Free Statistical Tests*, Prentice Hall, Englewood Cliffs, New Jersey, 1968.

Olmstead, P.S., Distribution of sample arrangements for runs up and down, *Annals of Mathematical Statistics*, *17*, 24-33, 1946.

Wallis, W.A., and G.H. Moore, A significance test for time series, *J. Amer. Statist. Assoc*., *36*, 401-409, 1941.

Young, L.C., On randomness in ordered sequences, *Annals of Mathematical Statistics*, *12*, 153-162, 1941.

See, in particular, Chapter 25 of:

Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsNPNominalSRTest](/igorpro/commands/statsnpnominalsrtest.md), [StatsRunsCDF](/igorpro/commands/statsrunscdf.md)

### *Demos* {#demos}
[Open Serial Randomness Demo.pxp](#igor-pxp/Examples/Statistics/Serial__Randomness__Demo.pxp)