---
description: "The StatsVariancesTest operation performs Bartlett's or Levene's test to determine if wave variances are equal."
slug: /commands/statsvariancestest
---

<div className="command-signature">

## <strong>StatsVariancesTest</strong>  [/ALPH=<em>val</em> /Q/Z/METH=<em>m</em> /WSTR=<em>strList</em> ]  [<em>wave1</em>, <em>wave2</em>,... <em>wave100</em> ] {#statsvariancestest}

</div>

The StatsVariancesTest operation performs Bartlett's or Levene's test to determine if wave variances are equal. Output is to the W_StatsVariancesTest wave in the current data folder or optionally to a table.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/DEST = *vWave*</span> | Specify the output wave for the variances test.  If you do not specify this flag, the operation saves the output in the wave W_StatsVariancesTest in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/METH = *m*</span> | Specifies the test type. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Bartlett test (default).</td></tr><tr><td>*m*&nbsp;=1:</td><td>Levene&#39;s test using the mean.</td></tr><tr><td>*m*&nbsp;=2:</td><td>Modified Levene&#39;s test using the median.</td></tr><tr><td>*m*&nbsp;=3:</td><td>Modified Levene&#39;s test using the 10% trimmed mean.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
|  | The table is associated with the test, not the data. If you repeat the test, it will update any existing table with the new results. |
| <span class="table-cell-nowrap">/WSTR = *waveListString*</span> |  |
|  | Specifies a string containing a semicolon-separated list of waves that contain sample data. Use *waveListString* instead of listing each wave after the flags. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
All tests define the null hypothesis by

$$
\displaystyle H_{0}: \quad \sigma_{1}^{2}=\sigma_{2}^{2}=\ldots=\sigma_{k}^{2},
$$

agains the alternative

$$
\displaystyle H_{a}: \quad \sigma_{i}^{2} \neq \sigma_{j}^{2} \text { for at least one } i \neq j .
$$

Bartlett's test computes:

$$
T=\frac{(n-k) \ln \left(\sigma_{w}^{2}\right)-\displaystyle \sum_{i=1}^{k}\left(n_{i}-1\right) \ln \left(\sigma_{i}^{2}\right)}{1+\displaystyle \frac{1}{3(k-1)}\left[\sum_{i=1}^{k} \frac{1}{n_{i}-1}-\frac{1}{N-k}\right]} .
$$

where 
$$
\displaystyle \sigma_{i}^{2}
$$
 is the variance of the *i* th wave, *N* is the sum of the points of all the waves, *n*<sub>i</sub>  is the number of points in wave *i*, and *k* is the number of waves. The weighted variance is given by

$$
\displaystyle \sigma_{w}^{2}=\sum_{i=1}^{k} \frac{\left(n_{i}-1\right) \sigma_{i}^{2}}{N-k}
$$

H<sub>0</sub> is rejected if T is greater than the critical value taken from the 
$$
\displaystyle \chi^{2}
$$
 distribution computed by solving for *x*:

$$
\displaystyle 1- { alpha }=1-{ gammq }\left(\frac{k-1}{2}, \frac{x}{2}\right) .
$$

Levene's test computes:

$$
W=\frac{(N-k) \displaystyle \sum_{i=1}^{k} n_{i}\left(\bar{Z}_{i}-\bar{Z}\right)^{2}}{(k-1) \displaystyle \sum_{i=1}^{k} \sum_{j=1}^{k}\left(Z_{i j}-\bar{Z}_{i}\right)^{2}},
$$

where

$$
\begin{array}{l}
Z_{i j}=\left|Y_{i j}-\bar{Y}_{i}\right|, \\
\\
\displaystyle \bar{Z}_{i}=\frac{1}{n_{i}} \sum_{j=1}^{k} Z_{i j}, \\
\\
\displaystyle \bar{Z}=\frac{1}{N} \sum_{i=1}^{k} \sum_{j=1}^{k} Z_{i j} .
\end{array}
$$

$$
\displaystyle \bar{Y}_{i}
$$
 depends on /METH.

H<sub>0</sub> is rejected if *W* is greater than the critical value from the F distribution computed by solving for *x*:

$$
\displaystyle 1-\text { alpha }=1-\text { betai }\left(\frac{v_{2}}{2}, \frac{v_{1}}{2}, \frac{v_{2}}{v_{2}+v_{1} x}\right) .
$$

### *References* {#references}
NIST/SEMATECH, Bartlett's Test, in *NIST/SEMATECH e-Handbook of Statistical Methods*, [http://www.itl.nist.gov/div898/handbook/eda/section3/eda357.htm](http://www.itl.nist.gov/div898/handbook/eda/section3/eda357.htm), 2005.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md)

### *Demos* {#demos}
[Open Variances-Test Demo.pxp](#igor-pxp/Examples/Statistics/Variances-Test__Demo.pxp)