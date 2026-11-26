---
description: "Returns the beta probability distribution function (PDF) given by $$ \\displaystyle F(x;p,q,a,b)=\\frac{({x - a})^{p - 1}(b-x)^{q-1}}{B(p, q)(b-a)^{p+q-1}}…"
slug: /commands/statsbetapdf
---

<div className="command-signature">

## <strong>StatsBetaPDF</strong> (<em>x</em>, <em>p</em>, <em>q</em> [, <em>a</em>, <em>b</em>]) {#statsbetapdf}

</div>

Returns the beta probability distribution function (PDF) given by

$$
\displaystyle F(x;p,q,a,b)=\frac{({x - a})^{p - 1}(b-x)^{q-1}}{B(p, q)(b-a)^{p+q-1}}, \quad \begin{array}{c} a \leq x \leq b \\ p,q > 0 \end{array}
$$

where *B*(*p*,*q*) is the beta function

$$
\displaystyle B(p, q)=\int_{0}^{1} t^{p-1}(1-t)^{q-1} d t.
$$

The defaults (*a* =0 and *b* =1) correspond to the standard beta distribution were *a* is the location parameter, (*b* -*a* ) is the scale parameter, and *p* and *q* are shape parameters. When *p* <1 *f* (*x* =*a* ) returns Inf.

### *References* {#references}
Evans, M., N. Hastings, and B. Peacock, *Statistical Distributions*, 3rd ed., Wiley, New York, 2000.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsBetaCDF](/igorpro/commands/statsbetacdf.md), [StatsInvBetaCDF](/igorpro/commands/statsinvbetacdf.md)