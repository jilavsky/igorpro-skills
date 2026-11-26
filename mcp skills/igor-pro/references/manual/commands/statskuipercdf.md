---
description: "The StatsKuiperCDF function returns the Kuiper cumulative distribution function."
slug: /commands/statskuipercdf
---

<div className="command-signature">

## <strong>StatsKuiperCDF</strong> (<em>V</em>) {#statskuipercdf}

</div>

The StatsKuiperCDF function returns the Kuiper cumulative distribution function

$$
\displaystyle F(V)=1-2 \sum_{j=1}^{\infty}\left(4 j^{2} V^{2}-1\right) \exp \left(-2 j^{2} V^{2}\right) .
$$

Accuracy is on the order of 1e-15. It returns 0 for values of *V* <0.4 or 1 for *V* >3.1.

### *References* {#references}
See in particular Section 14.3 of

Press, William H., et al., *Numerical Recipes in C*, Cambridge University Press, New York, 1992.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsInvKuiperCDF](/igorpro/commands/statsinvkuipercdf.md)