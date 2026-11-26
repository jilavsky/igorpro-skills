---
description: "The StatsInvKuiperCDF function returns the inverse of Kuiper cumulative distribution function."
slug: /commands/statsinvkuipercdf
---

<div className="command-signature">

## <strong>StatsInvKuiperCDF</strong> (<em>cdf</em>) {#statsinvkuipercdf}

</div>

The StatsInvKuiperCDF function returns the inverse of Kuiper cumulative distribution function.

There is no closed form expression. It is mapped to the range of 0.4 to 4, with accuracy of 1e-10.

### *References* {#references}
See in particular Section 14.3 of

Press, William H., et al., *Numerical Recipes in C*, Cambridge University Press, New York, 1992.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsKuiperCDF](/igorpro/commands/statskuipercdf.md)