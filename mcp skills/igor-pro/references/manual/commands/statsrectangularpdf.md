---
description: "The StatsRectangularPDF function returns the rectangular (uniform) probability distribution function."
slug: /commands/statsrectangularpdf
---

<div className="command-signature">

## <strong>StatsRectangularPDF</strong> (<em>x</em>, <em>a</em>, <em>b</em>) {#statsrectangularpdf}

</div>

The StatsRectangularPDF function returns the rectangular (uniform) probability distribution function.

$$
f(x ; a, b)=\left\{\begin{array}{ll}
\displaystyle \frac{1}{b-a} & a \leq x \leq b \\
\\
0 & \text { otherwise }
\end{array}\right.
$$

where *a* < *b*.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsRectangularCDF](/igorpro/commands/statsrectangularcdf.md), [StatsInvRectangularCDF](/igorpro/commands/statsinvrectangularcdf.md)