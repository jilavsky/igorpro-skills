---
description: "The StatsCircularTwoSampleTest operation peforms a number of tests for two samples of circular data."
slug: /commands/statscircularcorrelationtest
---

<div className="command-signature">

## <strong>StatsCircularCorrelationTest</strong>  [/ALPH=<em>alpha</em>  /T=<em>k</em> /NAA/PAA/PAL/Z/Q] <em>waveA</em>, <em>waveB</em> {#statscircularcorrelationtest}

</div>

The StatsCircularTwoSampleTest operation peforms a number of tests for two samples of circular data. Using the appropriate flags you can choose between parametric or nonparametric, unordered or paired tests. The input consists of two waves that contain one or two columns. The first column contains angle data expressed in radians and an optional second column contains associated vector lengths. The waves must be either single or double precision floating point. Results are stored in the W_StatsCircularCorrelationTest wave in the current data folder and optionally displayed in a table. Some flags generate additional outputs, described below.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default 0.05). |
| <span class="table-cell-nowrap">/NAA</span> | Performs a nonparametric angular-angular correlation test. |
| <span class="table-cell-nowrap">/PAA</span> | Performs a parametric angular-angular correlation test. |
| <span class="table-cell-nowrap">/PAL</span> | Performs a parametric angular-linear correlation test. In this case the angle wave is *waveA*  and the linear data corresponds to *waveB*. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. k specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. |

### *Details* {#details}
The nonparametric test (/NAA) follows Fisher and Lee's modification of Mardia's statistic, which is an analogue of Spearman's rank correlation. The test ranks the angles of each sample and computes the quantities *r*' and *r*'' as follows:

$$
r^{\prime}=\frac{\displaystyle \left\{\sum_{i=0}^{n-1} \cos \left[\frac{2 \pi}{n}\left(r_{a i}-r_{b i}\right)\right]\right\}^{2}+\left\{\sum_{i=0}^{n-1} \sin \left[\frac{2 \pi}{n}\left(r_{a i}-r_{b i}\right)\right]\right\}^{2}}{n^{2}},
$$

$$
r^{\prime \prime}=\frac{\displaystyle \left\{\sum_{i=0}^{n-1} \cos \left[\frac{2 \pi}{n}\left(r_{a i}+r_{b i}\right)\right]\right\}^{2}+\left\{\sum_{i=0}^{n-1} \sin \left[\frac{2 \pi}{n}\left(r_{a i}+r_{b i}\right)\right]\right\}^{2}}{n^{2}} .
$$

Here *n*  is the number of data pairs and *r*<sub>ai</sub><sub> </sub> and *r*<sub>bi</sub>  are the ranks of the *i*th member in the first and second samples respectively.

The test statistic is (*n*-1)(*r*'-*r*''), which is compared with the critical value (for one and two tails). The CDF of the statistic is a highly irregular function. The critical value is computed by a different methods according to *n*. For 3 <= *n* <= 8, a built-in table of CDF transitions gives a "conservative" estimate of the critical value. For 9 <= *n* <= 30, the CDF is approximated by a 7th order polynomial in the region x > 0. For *n* >= 30, the CDF is from the asymptotic expression. For 3 <= *n* <= 30, CDF values are obtained by Monte-Carlo simulations using 1e6 random samples for each *n*.

The parametric test for angular-angular correlation (/PAA) involves computation of a correlation coefficient *r*<sub>aa</sub>  and then evaluating the mean 
$$
\displaystyle \overline{r_{a a}}
$$
 and variance 
$$
\displaystyle S_{r_{a a}}^{2}
$$
of equivalent correlation coefficients computed from the same data but by deleting a different pair of angles each time. The mean and variance are then used to compute confidence limits L1 and L2:

$$
L 1=n r_{a a}-(n-1) \overline{r_{a a}}-Z_{\alpha(2)} \sqrt{\displaystyle \frac{s_{r_{a a}}^{2}}{n}},
$$

$$
L 2=n r_{a a}-(n-1) \overline{r_{a a}}+Z_{\alpha(2)} \sqrt{\displaystyle \frac{s_{r_{a a}}^{2}}{n}}
$$

where 
$$
\displaystyle Z_{\alpha(2)}
$$
 is the normal distribution two-tail critical value at the a level of significance. H<sub>0</sub> (corresponding to no correlation) is rejected if zero is not contained in the interval [L1,L2].

The parametric test for angular-linear correlation (/PAL) involves computation of the correlation coefficient *r*<sub>al</sub>  which is then compared with a critical value from 
$$
\displaystyle \chi^{2}
$$
for alpha significance and two degrees of freedom.

$$
\displaystyle r_{a l}=\sqrt{\frac{r_{x c}^{2}+r_{x s}^{2}-2 r_{x c} r_{x s} r_{c s}}{1-r_{c s}^{2}}},
$$

where:

$$
r_{x c}=\frac{\displaystyle \sum_{i=0}^{n-1} X_{i} \cos \left(a_{i}\right)-\frac{1}{n} \sum_{i=0}^{n-1} X_{i} \sum_{i=0}^{n-1} \cos \left(a_{i}\right)}{\displaystyle \sqrt{\left(\sum_{i=0}^{n-1} X_{i}^{2}-\frac{1}{n}\left(\sum_{i=0}^{n-1} X_{i}\right)^{2}\right)\left(\sum_{i=0}^{n-1} \cos ^{2}\left(a_{i}\right)-\frac{1}{n}\left(\sum_{i=0}^{n-1} \cos \left(a_{i}\right)\right)^{2}\right)}},
$$

$$
r_{x s}=\frac{\displaystyle \sum_{i=0}^{n-1} X_{i} \sin \left(a_{i}\right)-\frac{1}{n} \sum_{i=0}^{n-1} X_{i} \sum_{i=0}^{n-1} \sin \left(a_{i}\right)}{\sqrt{\displaystyle \left(\sum_{i=0}^{n-1} X_{i}^{2}-\frac{1}{n}\left(\sum_{i=0}^{n-1} X_{i}\right)^{2}\right)\left(\sum_{i=0}^{n-1} \sin ^{2}\left(a_{i}\right)-\frac{1}{n}\left(\sum_{i=0}^{n-1} \sin \left(a_{i}\right)\right)^{2}\right)}},
$$

$$
r_{c s}=\frac{\displaystyle \sum_{i=0}^{n-1} \cos \left(a_{i}\right) \sin \left(a_{i}\right)-\frac{1}{n} \sum_{i=0}^{n-1} \sin \left(a_{i}\right) \sum_{i=0}^{n-1} \cos \left(a_{i}\right)}{\displaystyle \sqrt{\left(\sum_{i=0}^{n-1} \sin ^{2}\left(a_{i}\right)-\frac{1}{n}\left(\sum_{i=0}^{n-1} \sin \left(a_{i}\right)\right)^{2}\right)\left(\sum_{i=0}^{n-1} \cos ^{2}\left(a_{i}\right)-\frac{1}{n}\left(\sum_{i=0}^{n-1} \cos \left(a_{i}\right)\right)^{2}\right)}} .
$$

### *References* {#references}
Fisher, N.I., and A.J. Lee, Nonparametric measures of angular-angular association, *Biometrica*, *69*, 315-321, 1982.

Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsInvChiCDF](/igorpro/commands/statsinvchicdf.md), [StatsInvNormalCDF](/igorpro/commands/statsinvnormalcdf.md), [StatsKendallTauTest](/igorpro/commands/statskendalltautest.md)

### *Demos* {#demos}
[Open Circular Correlation Demo.pxp](#igor-pxp/Examples/Statistics/Circular__Statistics/Circular__Correlation__Demo.pxp)