---
description: "The StatsQuantiles operation computes quantiles and elementary univariate statistics for a set of data in srcWave."
slug: /commands/statsquantiles
---

<div className="command-signature">

## <strong>StatsQuantiles</strong>  [/ALL/BOX/iNaN/IW/TM/Z/Q/QM=<em>method</em> /STBL/TRIM=<em>tValue</em> ] <em>srcWave</em> {#statsquantiles}

</div>

The StatsQuantiles operation computes quantiles and elementary univariate statistics for a set of data in *srcWave*.

**Flags**


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALL</span> | Invokes all flags except /Q, /QM, and /Z. |
| <span class="table-cell-nowrap">/BOX</span> | Computes parameters necessary to construct a box plot. |
| <span class="table-cell-nowrap">/DSTI = *qiWave*</span> | Specify the output wave for the quantile index (see /IW flag).  If you do not specify this flag, the operation stores the output in the wave W_QuantilesIndex in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTQ = *qWave*</span> | Specify the output wave for the quantile value wave (see /QW flag).  If you do not specify this flag, the operation stores the output in the wave W_QuantileValues in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DEST = *tWave*</span> | Specify the output wave for the statistical output that is normally displayed in a table.  If you do not specify this flag, the operation saves the output in the wave W_StatsQuantiles in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the specified destination waves as free waves. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/iNaN</span> | Ignores NaNs, which are sorted to the end of the array by default. |
| <span class="table-cell-nowrap">/IW</span> | Creates an index wave W_QuantilesIndex. W_QuantilesIndex[*i* ] corresponds to the position of *srcWave* [*i* ] when sorted from minimum to maximum. |
| <span class="table-cell-nowrap">/Q</span> | No information printed in the history area. |
| <span class="table-cell-nowrap">/QM = *qMethod*</span> | Specifies the method for computing quartiles. |
|  |<table class="nested-table"><tbody><tr><td>*qMethod*&nbsp;=0:</td><td>Tukey (default).</td></tr><tr><td>*qMethod*&nbsp;=1:</td><td>Minitab.</td></tr><tr><td>*qMethod*&nbsp;=2:</td><td>Moore and McCabe.</td></tr><tr><td>*qMethod*&nbsp;=3:</td><td>Mendenhall and Sincich.</td></tr></tbody></table>
|  | See Details for more information. |
| <span class="table-cell-nowrap">/QW</span> | Creates a single precision wave W_QuantileValues containing the quantile value corresponding to each entry in *srcWave*. |
| <span class="table-cell-nowrap">/STBL</span> | Uses a stable sort, which may require significant computation time for multiple entries with the same value. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays the result wave W_StatsQuantiles in a table and specifies window behavior when the user attempts to close the table. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
|  | If you use /K=2 you can still kill the window using the [KillWindow](/igorpro/commands/killwindow.md) operation. |
|  | This flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/TM</span> | Computes the tri-mean: 0.25*(V_Q25+2*median+V_Q75). |
| <span class="table-cell-nowrap">/TRIM = *tVal*</span> | Computes the trimmed mean which is the mean value of the entries between the quantiles *tVal* (in %) and 100-*tVal*. By default *tVal*=25 and the trimmed mean corresponds to the midmean. |
| <span class="table-cell-nowrap">/Z</span> | Ignores any errors. |

### *Details* {#details}
StatsQuantiles produces quick five-number summaries or more detailed results for univariate data. Values are returned in the wave W_StatsQuantiles and in the variables:


|  |  |
| --- | --- |
| V_min | Minimum value. |
| V_max | Maximum value. |
| V_Median | Median value of the data. |
| V_Q25 | Lower quartile. |
| V_Q75 | Upper quartile. |
| V_IQR | Inter-quartile range V_Q75-VQ25, which is also known as the H-spread. |
| V_MAD | Median absolute deviation. |
| V_Mode | The most frequent value. |
|  | If there is a tie and several values have the highest frequency then the lowest value among them is returned as the mode. |
|  | If all values in *srcWave* are unique or if the number of points in *srcWave* is less than 3, V_Mode is set to NaN. |
|  | This output was added in Igor Pro 7.00. |

Entries in the wave W_StatsQuantiles depend on your choice of flags. Each row has a row label explicitly defining its value. If you use the /ALL flag, W_StatsQuantiles will contain the following row labels:

- minValue
- maxValue
- Median
- Q25
- Q75
- IQR
- lowerInnerFence
- lowerOuterFence
- upperInnerFence
- upperOuterFence
- triMean
- trimmedMean
- MedianAbsoluteDeviation

Otherwise, W_StatsQuantiles will contain the first five entries and any additionally requested value. You should always access values using the [Dimension Labels](/igorpro/igor-basics/multidimensional-waves.md#dimension-labels).

There is frequently some confusion in comparing statistical results computed by different programs because each may use a different definition of quartiles. You can specify the method of computing the quartiles as you prefer with the /QM flag. If you neglect to choose a method, StatsQuantiles uses Tukey's method, which computes quartiles (also called hinges) as the lower and upper median values between the median of the data and the edges of the array. The Moore and McCabe method is similar to Tukey's method except you do not include the median itself in computing the quartiles. Mendenhall and Sincich compute the quartiles using 1/4 and 3/4 of (numDataPoints+1) and round to the nearest integer (if the fraction part is exactly 0.5 they round up for the lower quartile and down for the upper quartile). Minitab uses the same expressions but instead of rounding it uses linear interpolation.

StatsQuantiles uses a stable index sorting routine so that


```igor
IndexSort W_QuantilesIndex,srcWave
```

is a monotonically increasing wave.

### *References* {#references}
Tukey, J. W., *Exploratory Data Analysis*, 688 pp., Addison-Wesley, Reading, Massachusetts, 1977.

Mendenhall, W., and T. Sincich, *Statistics for Engineering and the Sciences*, 4th ed., 1008 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1995.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [WaveStats](/igorpro/commands/wavestats.md), [StatsMedian](/igorpro/commands/statsmedian.md), [median](/igorpro/commands/median.md), [Sort](/igorpro/commands/sort.md), [MakeIndex](/igorpro/commands/makeindex.md)