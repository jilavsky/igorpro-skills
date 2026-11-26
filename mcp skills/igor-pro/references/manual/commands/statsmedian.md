---
description: "The StatsMedian function returns the median value of a numeric wave waveName, which must not contain NaNs."
slug: /commands/statsmedian
---

<div className="command-signature">

## <strong>StatsMedian</strong> (<em>waveName</em>) {#statsmedian}

</div>

The StatsMedian function returns the median value of a numeric wave *waveName*, which must not contain NaNs

### *Example* {#example}

```igor
Make/N=5 sample1={1,2,3,4,5}
Print StatsMedian(sample1)
3
Make/N=6 sample2={1,2,3,4,5,6}
Print StatsMedian(sample2)
3.5
```

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [WaveStats](/igorpro/commands/wavestats.md), [StatsQuantiles](/igorpro/commands/statsquantiles.md), [median](/igorpro/commands/median.md)