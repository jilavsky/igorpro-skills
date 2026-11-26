---
description: "The StatsBetaCDF function returns the beta cumulative distribution function."
slug: /commands/statsbetacdf
---

<div className="command-signature">

## <strong>StatsBetaCDF</strong> (<em>x</em>, <em>p</em>, <em>q</em> [, <em>a</em>, <em>b</em>]) {#statsbetacdf}

</div>

The StatsBetaCDF function returns the beta cumulative distribution function

$$
\displaystyle F(x,p,q,a,b)=\frac{1}{{B}({p}, {q})} \int_{0}^{\frac{x-a}{b-a}} t^{p-1}(1-t)^{q-1} d t, \quad \begin{array}{c} p, q>0 \\ a \le x \le b \end{array}
$$

where *B*(*p*,*q*) is the beta function

$$
\displaystyle B(p, q)=\int_{0}^{1} t^{p-1}(1-t)^{q-1} d t.
$$

The defaults (*a* =0 and *b* =1) correspond to the standard beta distribution were *a* is the location parameter, (*b* -*a* ) is the scale parameter, and *p* and *q* are shape parameters.

### *References* {#references}
Evans, M., N. Hastings, and B. Peacock, *Statistical Distributions*, 3rd ed., Wiley, New York, 2000.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsBetaPDF](/igorpro/commands/statsbetapdf.md), [StatsInvBetaCDF](/igorpro/commands/statsinvbetacdf.md)