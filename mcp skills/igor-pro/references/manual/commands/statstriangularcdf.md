---
description: "The StatsTriangularCDF function returns the triangular cumulative distribution function."
slug: /commands/statstriangularcdf
---

<div className="command-signature">

## <strong>StatsTriangularCDF</strong> (<em>x</em>, <em>a</em>, <em>b</em>, <em>c</em>) {#statstriangularcdf}

</div>

The StatsTriangularCDF function returns the triangular cumulative distribution function.

$$
F(x ; a, b, c)=\left\{\begin{array}{cc}
0 & x \leq a \\
\\
\displaystyle \frac{(x-a)^{2}}{(b-a)(c-a)} & a<x \leq c \\
\\
1-\displaystyle \frac{(b-x)^{2}}{(b-a)(b-c)} & c<x<b \\
\\
1 & x \geq b
\end{array}\right.
$$

where *a* < *c* < *b.*

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsTriangularPDF](/igorpro/commands/statstriangularpdf.md), [StatsInvTriangularCDF](/igorpro/commands/statsinvtriangularcdf.md)