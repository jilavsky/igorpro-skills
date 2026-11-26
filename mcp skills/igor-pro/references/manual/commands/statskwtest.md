---
description: "The StatsKWTest operation performs the nonparametric Kruskal-Wallis test which tests variances using the ranks of the data."
slug: /commands/statskwtest
---

<div className="command-signature">

## <strong>StatsKWTest</strong>  [/ALPH=<em>significance</em> /Q/Z/T=<em>k</em> /WSTR=<em>wList</em> ] [<em>wave1</em>, <em>wave2</em>,... <em>wave100</em> ] {#statskwtest}

</div>

The StatsKWTest operation performs the nonparametric Kruskal-Wallis test which tests variances using the ranks of the data. Output is to the W_KWTestResults wave in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/DEST = *kwWave*</span> | Specify the destination wave for the nonparametric Kruskal-Wallis test results.  If you do not use this flag, the operation saves the output in the wave W_KWTestResults in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/E</span> | Computes the exact P-value using the Klotz and Teng algorithm, which may require long computation times for large data sets. You can stop the calculation by pressing the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations) after which all remaining results remain valid and the exact P-value is set to NaN. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/WSTR = *waveListString*</span> |  |
|  | Specifies a string containing a semicolon-separated list of waves that contain sample data. Use *waveListString* instead of listing each wave after the flags. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
Inputs are two or more 1D numerical waves (one for each group of samples). Use NaNs for missing data or use waves with different number of points.

StatsKWTest always computes the critical values using both the Chi-squared and Wallace approximations. If appropriate (small enough data set) you can also use /E to obtain the exact P value. When the calculation involves many waves or many data points the calculation of the exact critical value can be very lengthy. All the results are saved in the wave W_KWTestResults in the current data folder and are optionally displayed in a table (/T). The wave contains the following information:

| Row | Data |
| --- | --- |
| 0 | Number of groups |
| 1 | Number of valid data points (excludes NaNs) |
| 2 | Alpha |
| 3 | Kruskal-Wallis Statistic H |
| 4 | Chi-squared approximation for the critical value Hc |
| 5 | Chi-squared approximation for the P value |
| 6 | Wallace approximation for the critical value Hc |
| 7 | Wallace approximation for the P value |
| 8 | Exact P value (requires /E) |

H<sub>0</sub> for the Kruskal-Wallis test is that all input waves are the same. If the test fails and the input consisted of more than two waves, there is no indication for possible agreement between some of the waves. See [StatsNPMCTest](/igorpro/commands/statsnpmctest.md) for further analysis.

V_flag will be set to -1 for any error and to zero otherwise.

### *References* {#references}
Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

Wallace, D.L., Simplified Beta-Approximation To The Kruskal-Wallis H Test, *Jour. Am. Stat. Assoc.*, *54*, 225-230, 1959.

J.H. Klotz, *Computational Approach to Statistics*.

Klotz, J. and Teng, J. (1977). One-way layout for counts and the exact enumeration of the Kruskal-Wallis H distribution with ties. Journal of the American Statistical Association 72, 165-169.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsWilcoxonRankTest](/igorpro/commands/statswilcoxonranktest.md), [StatsNPMCTest](/igorpro/commands/statsnpmctest.md), [StatsAngularDistanceTest](/igorpro/commands/statsangulardistancetest.md)

### *Demos* {#demos}
[Open Kruskal-Wallis Demo.pxp](#igor-pxp/Examples/Statistics/Kruskal-Wallis__Demo.pxp)