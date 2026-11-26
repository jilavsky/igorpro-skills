---
description: "The StatsRectangularCDF function returns the rectangular (uniform) cumulative distribution function."
slug: /commands/statsrectangularcdf
---

<div className="command-signature">

## <strong>StatsRectangularCDF</strong> (<em>x</em>, <em>a</em>, <em>b</em>) {#statsrectangularcdf}

</div>

The StatsRectangularCDF function returns the rectangular (uniform) cumulative distribution function.

$$
F(x, a, b)=\left\{\begin{array}{ll}
0 & x \leq a \\
\\
\displaystyle \frac{x-a}{b-a} & a \leq x \leq b \\
\\
1 & x \geq b
\end{array}\right.
$$

where *a* < *b*.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsRectangularPDF](/igorpro/commands/statsrectangularpdf.md), [StatsInvRectangularCDF](/igorpro/commands/statsinvrectangularcdf.md)