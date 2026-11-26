---
description: "The StatsInvPowerCDF function returns the inverse of the Power Function cumulative distribution function."
slug: /commands/statsinvpowercdf
---

<div className="command-signature">

## <strong>StatsInvPowerCDF</strong> (<em>cdf</em>, <em>b</em>, <em>c</em>) {#statsinvpowercdf}

</div>

The StatsInvPowerCDF function returns the inverse of the Power Function cumulative distribution function

$$
\displaystyle x=b / cdf^{(1 / c)}
$$

where the scale parameter *b* and the shape parameter *c* satisfy *b,c* > 0.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsPowerPDF](/igorpro/commands/statspowerpdf.md), [StatsPowerCDF](/igorpro/commands/statspowercdf.md), [StatsPowerNoise](/igorpro/commands/statspowernoise.md)