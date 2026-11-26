---
description: "The StatsTrimmedMean function returns the mean of the wave waveName after removing trimValue fraction of the values from both tails of the distribution."
slug: /commands/statstrimmedmean
---

<div className="command-signature">

## <strong>StatsTrimmedMean</strong> (<em>waveName</em>, <em>trimValue</em>) {#statstrimmedmean}

</div>

The StatsTrimmedMean function returns the mean of the wave *waveName* after removing *trimValue* fraction of the values from both tails of the distribution. *trimValue* is a number in the range [0, 0.5]. *waveName* can be any real numeric type.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsQuantiles](/igorpro/commands/statsquantiles.md), [mean](/igorpro/commands/mean.md)