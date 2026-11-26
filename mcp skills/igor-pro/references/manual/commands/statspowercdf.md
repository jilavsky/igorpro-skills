---
description: "The StatsPowerCDF function returns the Power Function cumulative distribution function."
slug: /commands/statspowercdf
---

<div className="command-signature">

## <strong>StatsPowerCDF</strong> (<em>x</em>, <em>b</em>, <em>c</em>) {#statspowercdf}

</div>

The StatsPowerCDF function returns the Power Function cumulative distribution function.

$$
\displaystyle F(x ; b, c)=\left(\frac{x}{b}\right)^{c}.
$$

where the scale parameter *b* and the shape parameter *c* satisfy *b,c* > 0 and b>=*x*>=*0*.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsPowerPDF](/igorpro/commands/statspowerpdf.md), [StatsInvPowerCDF](/igorpro/commands/statsinvpowercdf.md), [StatsPowerNoise](/igorpro/commands/statspowernoise.md)