---
description: "The StatsRunsCDF function returns the cumulative distribution function for the up and down runs distribution for total number of runs r in a random linear…"
slug: /commands/statsrunscdf
---

<div className="command-signature">

## <strong>StatsRunsCDF</strong> (<em>n</em>, <em>r</em>) {#statsrunscdf}

</div>

The StatsRunsCDF function returns the cumulative distribution function for the up and down runs distribution for total number of runs *r* in a random linear arrangement of *n* unequal elements. There is no closed form expression. It is computed numerically from the recursion of the probability density

$$
\displaystyle f(r, n)=\frac{r f(r, n-1)+2 f(r-1, n-1)+(n-r) f(r-2, n-1)}{n},
$$

with the intial condition

$$
\displaystyle f(1, n)=\frac{2}{n!} .
$$

### *References* {#references}
Bradley, J.V., *Distribution-Free Statistical Tests*, Prentice Hall, Englewood Cliffs, New Jersey, 1968.

Olmstead, P.S., Distribution of sample arrangements for runs up and down, *Annals of Mathematical Statistics*, *17*, 24-33, 1946..

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsSRTest](/igorpro/commands/statssrtest.md)