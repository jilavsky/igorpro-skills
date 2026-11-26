---
description: "The StatsInvTriangularCDF function returns the inverse of the triangular cumulative distribution function."
slug: /commands/statsinvtriangularcdf
---

<div className="command-signature">

## <strong>StatsInvTriangularCDF</strong> (<em>cdf</em>, <em>a</em>, <em>b</em>, <em>c</em>) {#statsinvtriangularcdf}

</div>

The StatsInvTriangularCDF function returns the inverse of the triangular cumulative distribution function

$$
x=\left\{\begin{array}{ll}
a+\sqrt{c d f(b-a)(c-a)} & 0 \leq c d f \leq \displaystyle \frac{c-a}{b-a} \\
\\
b-\sqrt{(1-c d f)(b-a)(b-c)} & \displaystyle \frac{c-a}{b-a} \leq c d f \leq 1
\end{array}\right.
$$

where *a* < *c* < *b.*

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsTriangularPDF](/igorpro/commands/statstriangularpdf.md), [StatsTriangularCDF](/igorpro/commands/statstriangularcdf.md)