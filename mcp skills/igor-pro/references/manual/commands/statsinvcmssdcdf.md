---
description: "The StatsInvCMSSDCDF function returns the critical values of the C distribution (mean square successive difference distribution), which is given by."
slug: /commands/statsinvcmssdcdf
---

<div className="command-signature">

## <strong>StatsInvCMSSDCDF</strong> (<em>cdf</em>, <em>n</em>) {#statsinvcmssdcdf}

</div>

The StatsInvCMSSDCDF function returns the critical values of the C distribution (mean square successive difference distribution), which is given by

$$
\displaystyle f(C, n)=\frac{\Gamma(2 m+2)}{a 2^{2 m+1}[\Gamma(m+1)]^{2}}\left(1-\frac{C^{2}}{a^{2}}\right)^{m},
$$

where

$$
\displaystyle a^{2}=\frac{\left(n^{2}+2 n-12\right)(n-2)}{\left(n^{3}-13 n+24\right)},
$$

$$
\displaystyle m=\frac{\left(n^{4}-n^{3}-13 n^{2}+37 n-60\right)}{2\left(n^{3}-13 n+24\right)} .
$$

Critical values are computed from the integral of the probability distribution function.

### *References* {#references}
Young, L.C., On randomness in ordered sequences, *Annals of Mathematical Statistics*, *12*, 153-162, 1941.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsCMSSDCDF](/igorpro/commands/statscmssdcdf.md), [StatsSRTest](/igorpro/commands/statssrtest.md)