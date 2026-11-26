---
description: "The StatsPowerPDF function returns the Power Function probability distribution function."
slug: /commands/statspowerpdf
---

<div className="command-signature">

## <strong>StatsPowerPDF</strong> (<em>x</em>, <em>b</em>, <em>c</em>) {#statspowerpdf}

</div>

The StatsPowerPDF function returns the Power Function probability distribution function

$$
\displaystyle f(x, b, c)=\frac{|c|}{x}\left(\frac{\mathrm{x}}{b}\right)^{c},
$$

where b is a scale parameter and c is a shape parameter.

For b,c > 0, x is drawn from b >= x >= 0.

For b>0, c<0, x is drawn from x>b.

For b<0, c>0, x is drawn from -b <= x <= 0.

For b<0, c<0, x is drawn from x<-b.

Note that for -1<c<0 the average diverges and the magnitude of a mean calculated from N samples will increase indefinitely with N.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsPowerCDF](/igorpro/commands/statspowercdf.md), [StatsInvPowerCDF](/igorpro/commands/statsinvpowercdf.md), [StatsPowerNoise](/igorpro/commands/statspowernoise.md)