---
description: "The StatsGEVPDF function returns the generalized extreme value probability distribution function."
slug: /commands/statsgevpdf
---

<div className="command-signature">

## <strong>StatsGEVPDF</strong> (<em>x</em>, µ, σ, ξ) {#statsgevpdf}

</div>

The StatsGEVPDF function returns the generalized extreme value probability distribution function.

$$
\displaystyle f(x, \mu, \sigma, \xi)=\frac{1}{\sigma}\left[1+\xi\left(\frac{x-\mu}{\sigma}\right)\right]^{(-1 / \xi)-1} \exp \left\{-\left[1+\xi\left(\frac{x-\mu}{\sigma}\right)^{-1 / \xi}\right]\right\},
$$

where

$$
\displaystyle 1+\xi\left(\frac{x-\mu}{\sigma}\right)>0,
$$

and σ>0.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsGEVCDF](/igorpro/commands/statsgevcdf.md), [StatsEValuePDF](/igorpro/commands/statsevaluepdf.md), [StatsEValueCDF](/igorpro/commands/statsevaluecdf.md), [StatsInvEValueCDF](/igorpro/commands/statsinvevaluecdf.md)