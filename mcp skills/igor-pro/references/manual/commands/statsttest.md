---
description: "The StatsTTest operation performs two kinds of T-tests: the first compares the mean of a distribution with a specified mean value (/MEAN) and the second…"
slug: /commands/statsttest
---

<div className="command-signature">

## <strong>StatsTTest</strong>  [/ALPH=<em>alpha</em>  /CI /DFM=<em>m</em>  /MEAN=<em>meanV</em>  /PAIR /TAIL=<em>n</em>  /T=<em>k</em> /Z /Q] <em>wave1</em>  [, <em>wave2</em> ] {#statsttest}

</div>

The StatsTTest operation performs two kinds of T-tests: the first compares the mean of a distribution with a specified mean value (/MEAN) and the second compares the means of the two distributions contained in wave1 and wave2, which must contain at least two data points, can be any real numeric type, and can have an arbitrary number of dimensions. Output is to the W_StatsTTest wave in the current data folder or optionally to a table.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/CI</span> | Computes the confidence intervals for the mean(s). |
| <span class="table-cell-nowrap">/DEST = *tWave*</span> | Specify the output wave for the T-Test.  If you do not specify this flag, the operation saves the output in the wave  W_StatsTTest in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DFM = *m*</span> | Specifies method for calculating the degrees of freedom. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Default; computes equivalent degrees of freedom accounting for possibly different variances.</td></tr><tr><td>*m*&nbsp;=1:</td><td>Computes equivalent degrees of freedom but truncates to a smaller integer.</td></tr><tr><td>*m*&nbsp;=2:</td><td>Computes degrees of freedom by</td></tr><tr><td></td><td>$$ \displaystyle D F=n_{1}+n_{2}-2 $$</td></tr><tr><td></td><td>where *n* is the sum of points in the wave. Appropriate when variances are equal.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/FREE</span> | Creates the specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/MEAN = *meanV*</span> | Compares meanV with the mean of the distribution in *wave1*. Outputs are the number of points in the wave, the degrees of freedom (accounting for any NaNs), the average, standard deviation (σ), |
|  | $$ \displaystyle s_{\bar{X}}=\frac{\sigma}{\sqrt{D F+1}}, $$ |
|  | the statistic |
|  | $$ \displaystyle t=\frac{\bar{X}-\text { mean } V}{s_{\bar{X}}} $$ |
|  | and the critical value, which depends on /TAIL. |
| <span class="table-cell-nowrap">/PAIR</span> | Specifies that the input waves are pairs and computes the difference of each pair of data to get the average difference $$ \displaystyle \bar{d} $$and the standard error of the difference $$ \displaystyle S_{\bar{d}} $$.  The t statistic is the ratio of the two |
|  | $$ \displaystyle t=\frac{\bar{d}}{s_{\bar{d}}} . $$ |
|  | In this case H<sub>0</sub> is that the difference $$ \displaystyle \bar{d} $$ is zero. |
|  | This mode does not support /CI and /DFM. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
|  | The table is associated with the test, not the data. If you repeat the test, it will update any existing table with the new results. |
| <span class="table-cell-nowrap">/TAIL = *tailCode*</span> | Specifies H<sub>0</sub>. |
|  |<table class="nested-table"><tbody><tr><td>*tailCode*&nbsp;=1:</td><td>One tailed test (µ<sub>1</sub> &lt;= µ<sub>2</sub>).</td></tr><tr><td>*tailCode*&nbsp;=&nbsp;2:</td><td>One tailed test (µ<sub>1</sub> &gt;= µ<sub>2</sub>).</td></tr><tr><td>*tailCode*&nbsp;=4:</td><td>Default; two tailed test (µ<sub>1</sub> = µ<sub>2</sub>).</td></tr></tbody></table>
|  | When performing paired tests using /PAIR: |
|  |<table class="nested-table"><tbody><tr><td>*tailCode*&nbsp;=1:</td><td>One tailed test (µ<sub>d</sub> &lt;= 0).</td></tr><tr><td>*tailCode*&nbsp;=&nbsp;2:</td><td>One tailed test (µ<sub>d</sub> &gt;= 0).</td></tr><tr><td>*tailCode*&nbsp;=4:</td><td>Default; two tailed test (µ<sub>d</sub> = 0).</td></tr></tbody></table>
|  | Here µ<sub>d</sub> is the mean of the difference population. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
When comparing the mean of a single distribution with a hypothesized mean value, you should use /MEAN and only one wave (*wave1* ). If you use two waves StatsTTest performs the T-test for the means of the corresponding distributions (which is incompatible with /MEAN).

When comparing the means of two distributions, the default t-statistic is computed from Welch's approximate t:

$$
t^{\prime}=\frac{\bar{x}_{1}-\bar{x}_{2}}{\displaystyle \sqrt{\frac{s_{1}^{2}}{n_{1}}+\frac{s_{2}^{2}}{n_{2}}}},
$$

where 
$$
\displaystyle s_{i}^{2}
$$
 are variances, n<sub>i</sub> are the number of samples and 
$$
\displaystyle \bar{X}_{i}
$$
 are the averages of the respective waves. This expression is appropriate when the number of points and the variances of the two waves are different. If you want to compute the t-statistic using pooled variance you can use the /AEVR flag. In this case the pooled variance is given by

$$
\displaystyle s_{p}^{2}=\frac{\left(n_{1}-1\right) s_{1}^{2}+\left(n_{2}-1\right) s_{2}^{2}}{n_{1}+n_{2}-2},
$$

and the t-statistic is

$$
\displaystyle t=\frac{\bar{x}_{1}-\bar{x}_{2}}{s_{p} \sqrt{\frac{1}{n_{1}}+\frac{1}{n_{2}}}} .
$$

The different test are:

| H<sub>0</sub> | Rejection Condition |
| --- | --- |
| µ<sub>1</sub>=µ<sub>2</sub> | \|t\| >= Tc(alpha,ν) |
| µ<sub>1</sub>>µ<sub>2</sub> | t <= Tc(alpha, ν) |
| µ<sub>1</sub><µ<sub>2</sub> | t >= Tc(alpha, ν) |

*Tc* is the critical value and *ν* is the effective number of degrees of freedom (see /DFM flag). When accounting for possibly unequal variances, *ν* is given by

$$
v=\frac{\left(\displaystyle \frac{s_{1}^{2}}{n_{1}}+\frac{\displaystyle s_{2}^{2}}{n_{2}}\right)^{2}}{\displaystyle \frac{\left(\displaystyle \frac{s_{1}^{2}}{n_{1}}\right)^{2}}{\displaystyle n_{1}-1}+\frac{\displaystyle \left(\frac{\displaystyle s_{2}^{2}}{n_{2}}\right)^{2}}{\displaystyle n_{2}-1}} .
$$

The critical values (Tc) are computed by numerically by solving for the argument at which the cumulative distribution function (CDF) equals the appropriate values for the tests. The CDF is given by

$$
F(x)=\left\{\begin{array}{ll}
\displaystyle \frac{1}{2} \text { betai }\left(\frac{v}{2}, \frac{1}{2}, \frac{v}{v+x^{2}}\right) & x<0 \\
\\
\displaystyle 1-\frac{1}{2} \text { betai }\left(\frac{v}{2}, \frac{1}{2}, \frac{v}{v+x^{2}}\right) & x \geq 0
\end{array}\right.
$$

To get the critical value for the upper one-tail test we solve F(x)=1-alpha.  For the lower one-tail test we solve for x the equation F(x)=alpha. In the two-tailed test the lower critical value is a solution for F(x)=alpha/2 and the upper critical value is a solution for F(x)=1-alpha/2.

The T-test assumes that both samples are randomly taken from normally distributed populations.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsStudentPDF](/igorpro/commands/statsstudentpdf.md), [StatsStudentCDF](/igorpro/commands/statsstudentcdf.md), [StatsInvStudentCDF](/igorpro/commands/statsinvstudentcdf.md)

### *References* {#references}
Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.  See in particular Section 8.1.

### *Demos* {#demos}
[Open T-Test Demo.pxp](#igor-pxp/Examples/Statistics/T-Test__Demo.pxp)