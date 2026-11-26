---
description: "The StatsInvMooreCDF function returns the inverse cumulative distribution function for Moore's R*, which is used as a critical value in nonparametric version…"
slug: /commands/statsinvmoorecdf
---

<div className="command-signature">

## <strong>StatsInvMooreCDF</strong> (<em>cdf</em>, <em>N</em>) {#statsinvmoorecdf}

</div>

The StatsInvMooreCDF function returns the inverse cumulative distribution function for Moore's R*, which is used as a critical value in nonparametric version of the Rayleigh test for uniform distribution around the circle. It supports the range 3<=*N* <=120 and does not change appreciably for *N* >120.

The inverse distribution is computed from polynomial approximations derived from simulations and should be accurate to approximately three significant digits.

### *References* {#references}
Moore, B.R., A modification of the Rayleigh test for vector data, *Biometrica*, *67*, 175-180, 1980.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsCircularMeans](/igorpro/commands/statscircularmeans.md).