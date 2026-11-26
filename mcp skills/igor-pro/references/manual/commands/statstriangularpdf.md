---
description: "The StatsTriangularPDF function returns the triangular probability distribution function."
slug: /commands/statstriangularpdf
---

<div className="command-signature">

## <strong>StatsTriangularPDF</strong> (<em>x</em>, <em>a</em>, <em>b</em>, <em>c</em>) {#statstriangularpdf}

</div>

The StatsTriangularPDF function returns the triangular probability distribution function.

$$
f(x ; a, b, c)=\left\{\begin{array}{cc}
\displaystyle \frac{2(x-a)}{(b-a)(c-a)} & a \leq x<c \\
\\
\displaystyle \frac{2(b-x)}{(b-a)(b-c)} & c<x \leq b \\
\\
0 & \text { Otherwise }
\end{array}\right.
$$

where *a* < *c* < *b.*

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsTriangularCDF](/igorpro/commands/statstriangularcdf.md), [StatsInvTriangularCDF](/igorpro/commands/statsinvtriangularcdf.md)