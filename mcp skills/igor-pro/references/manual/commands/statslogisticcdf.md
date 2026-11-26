---
description: "The StatsLogisticCDF function returns the logistic cumulative distribution function."
slug: /commands/statslogisticcdf
---

<div className="command-signature">

## <strong>StatsLogisticCDF</strong> (<em>x</em>, <em>a</em>, <em>b</em>) {#statslogisticcdf}

</div>

The StatsLogisticCDF function returns the logistic cumulative distribution function

$$
F(x ; a, b)=\frac{1}{1+\exp \left(-\displaystyle \frac{x-a}{b}\right)} .
$$

Here the scale parameter *b* >0 and the shape parameter is *a*.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsLogisticPDF](/igorpro/commands/statslogisticpdf.md), [StatsInvLogisticCDF](/igorpro/commands/statsinvlogisticcdf.md)