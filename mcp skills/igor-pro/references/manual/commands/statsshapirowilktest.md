---
description: "The StatsShapiroWilkTest computes Shapiro-Wilk statistic W and its associated P-value and stores them in V_statistic and V_prob respectively."
slug: /commands/statsshapirowilktest
---

<div className="command-signature">

## <strong>StatsShapiroWilkTest</strong>  [/Q/Z] <em>srcWave</em> {#statsshapirowilktest}

</div>

The StatsShapiroWilkTest computes Shapiro-Wilk statistic W and its associated P-value and stores them in V_statistic and V_prob respectively.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. |

### *Details* {#details}
The Shapiro-Wilk tests the null hypothesis that the population is normally distributed. If the P-value is less than the selected alpha then the null hypothesis, normality, is rejected.

The test is valid only for waves containing 3 to 5000 data points. The operation ignores any NaNs or INFs in *srcWave.*

### *Example* {#example}

```igor
// Test normally distributed data	
Make/O/N=(200) ggg=gnoise(5)
StatsShapiroWilkTest ggg
W=0.995697	 p=0.846139	// p>alpha so accept normality

// Test uniform distribution
Make/O/N=(200) eee=enoise(5)
StatsShapiroWilkTest eee
W=0.959616	 p=1.7979e-05	// p<alpha so reject normality
```