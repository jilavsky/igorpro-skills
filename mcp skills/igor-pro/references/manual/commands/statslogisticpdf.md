---
description: "The StatsLogisticPDF function returns the logistic probability distribution function."
slug: /commands/statslogisticpdf
---

<div className="command-signature">

## <strong>StatsLogisticPDF</strong> (<em>x</em>, <em>a</em>, <em>b</em>) {#statslogisticpdf}

</div>

The StatsLogisticPDF function returns the logistic probability distribution function

$$
f(x ; a, b)=\frac{\displaystyle \exp \left(-\frac{x-a}{b}\right)}{\displaystyle b\left[1+\exp \left(-\frac{x-a}{b}\right)\right]^{2}},
$$

where the scale parameter *b* >0 and the shape parameter is *a*.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsLogisticCDF](/igorpro/commands/statslogisticcdf.md), [StatsInvLogisticCDF](/igorpro/commands/statsinvlogisticcdf.md)