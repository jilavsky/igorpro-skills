---
description: "The StatsGEVCDF function returns the generalized extreme value cumulative distribution function."
slug: /commands/statsgevcdf
---

<div className="command-signature">

## <strong>StatsGEVCDF</strong> (<em>x</em>, µ, σ, ξ) {#statsgevcdf}

</div>

The StatsGEVCDF function returns the generalized extreme value cumulative distribution function.

$$
\displaystyle F(x, \mu, \sigma, \xi)=\exp \left\{-\left[1+\xi\left(\frac{x-\mu}{\sigma}\right)^{-1 / \xi}\right]\right\},
$$

where

$$
\displaystyle 1+\xi\left(\frac{x-\mu}{\sigma}\right)>0,
$$

and σ>0.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsGEVPDF](/igorpro/commands/statsgevpdf.md), [StatsEValuePDF](/igorpro/commands/statsevaluepdf.md), [StatsEValueCDF](/igorpro/commands/statsevaluecdf.md), [StatsInvEValueCDF](/igorpro/commands/statsinvevaluecdf.md)