---
description: "The StatsWilcoxonRankTest operation performs the nonparametric Wilcoxon-Mann-Whitney two-sample rank test or the Wilcoxon Signed Rank test (for paired data)…"
slug: /commands/statswilcoxonranktest
---

<div className="command-signature">

## <strong>StatsWilcoxonRankTest</strong>  [/ALPH=<em>val</em> /APRX=<em>m</em> /T=<em>k</em> /TAIL=<em>tail</em> /Q/Z]  <em>waveA</em>, <em>waveB</em> {#statswilcoxonranktest}

</div>

The StatsWilcoxonRankTest operation performs the nonparametric Wilcoxon-Mann-Whitney two-sample rank test or the Wilcoxon Signed Rank test (for paired data) on *waveA* and *waveB*. Output is to the W_WilcoxonTest wave in the current data folder or optionally to a table.

Note that *waveA* and *waveB* must not contain NaNs or INFs.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/APRX = *m*</span> | Sets the approximation method. It computes an exact critical value by default. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=1:</td><td>Standard normal approximation with ties (Zar P. 151).</td></tr><tr><td>*m*&nbsp;=2:</td><td>Improved normal approximation (Zar P. 152).</td></tr></tbody></table>
|  | Approximations may be appropriate for large sample sizes when computation may take a long time. |
| <span class="table-cell-nowrap">/DEST = *wrWave*</span> | Specify the destination wave for the Wilcoxon-Mann-Whitney two-sample rank test results. If you do not use this flag, the operation saves the output in the wave W_WilcoxonTest in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
|  | The table is associated with the test, not the data. If you repeat the test, it will update any existing table with the new results. |
| <span class="table-cell-nowrap">/TAIL = *tail*</span> | Specifies the tail tested. |
|  |<table class="nested-table"><tbody><tr><td>*tail*&nbsp;=1:</td><td>Lower tail.</td></tr><tr><td>*tail*&nbsp;=2:</td><td>Upper tail.</td></tr><tr><td>*tail*&nbsp;=4:</td><td>Two tail.</td></tr></tbody></table>
|  | You can perform any combination of tests by adding their corresponding tail values (/TAIL=7 tests all tail possiblities). Note that H0 changes according to the selected tail. |
| <span class="table-cell-nowrap">/WSRT</span> | Performs the Wilcoxon Signed Rank Test for paired data. The test computes statistics Tp and Tm, lower-tail, upper-tail, and two-tail P-values. If the number of samples is less than 200 it computes exact P-values, otherwise they are computed using the normal approximation. Do not use /ALPH, /APRX, and /TAIL with this flag. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. |

### *Details* {#details}
The Wilcoxon-Mann-Whitney test combines the two samples and ranks them to compute the statistic *U*. If *waveA* has *m* points and *waveB* has *n* points, then *U* is given by

$$
\displaystyle U=m n+\frac{m(m+1)}{2}-R_{1},
$$

with the corresponding statistic *U'* given by

$$
\displaystyle U^{\prime}=n m+\frac{n(n+1)}{2}-R 2 .
$$

where *R*<sub>i</sub> is the sum of the ranks of data in the ith wave (ranked in ascending order).

The distribution of *U* is difficult to compute, requiring the number of possible permutations of *m* elements of *waveA* and *n* elements of *waveB* that give rise to *U* values that do not exceed the one computed. The distribution is computed according to the algorithm developed by Klotz. With increasing sample size one can avoid the time consuming distribution computation and use a normal approximation instead. Klotz recommends this approximation for

$$
\displaystyle \mathrm{N}=\mathrm{m}+\mathrm{n} \sim 100 .
$$

Use /APRX=2 for the best approximation. The two approximations are discussed by Zar.

The Wilcoxon Signed Rank Test, or Wilcoxon Paired-Sample Test, ranks the difference between pairs of values and computes the sums of the positive ranks (Tp) and the negative ranks (Tm). It calculates Tp and Tm and P-values for all tail combinations. The P-values are:

|  |  |
| --- | --- |
| P_lower_tail | P(Wp<=Tp) |
| P_upper_tail | P(Wp>=Tp) |
| P_two_tail | 2\*min(P_lower_tail, P_upper_tail) |

Wp is the generic symbol for the sum of positive ranks for the given number of pairs.

V_flag will be set to -1 for any error and to zero otherwise.

In both Wilcoxon-Mann-Whitney two-sample rank test and the Wilcoxon Signed Rank test H0 is that the data in the two input waves are statistically the same.

### *References* {#references}
Cheung, Y.K., and J.H. Klotz, The Mann Whitney Wilcoxon distribution using linked lists, *Statistica Sinica*, *7*, 805-813, 1997.

See in particular Chapter 15 of:

Klotz, J.H., *Computational Approach to Statistics*.

Streitberg, B., and J. Rohmel, Exact distributions for permutations and rank tests: An introduction to some recently published algorithms, *Statistical Software Newsletter*, *12*, 10-17, 1986.

Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsAngularDistanceTest](/igorpro/commands/statsangulardistancetest.md), [StatsKWTest](/igorpro/commands/statskwtest.md), [StatsSignTest](/igorpro/commands/statssigntest.md)

### *Demos* {#demos}
[Open Wilcoxon-Test Demo.pxp](#igor-pxp/Examples/Statistics/Wilcoxon-Test__Demo.pxp)