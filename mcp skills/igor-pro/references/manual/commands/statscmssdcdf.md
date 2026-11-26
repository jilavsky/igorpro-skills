---
description: "The StatsCMSSDCDF function returns the cumulative distribution function of the C distribution (mean square successive difference), which is."
slug: /commands/statscmssdcdf
---

<div className="command-signature">

## <strong>StatsCMSSDCDF</strong> (<em>C</em>, <em>n</em>) {#statscmssdcdf}

</div>

The StatsCMSSDCDF function returns the cumulative distribution function of the C distribution (mean square successive difference), which is

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

The distribution (for *C* >0) can then be expressed as

$$
\displaystyle F(C, n)=\frac{\Gamma(2 m+2)}{a 2^{2 m+1}[\Gamma(m+1)]^{2}} C_{2} F_{1}\left(\frac{1}{2},-m, \frac{3}{2}, \frac{C^{2}}{a^{2}}\right),
$$

where 
$$
\displaystyle { }_{2} F_{1}
$$
 is the Hypergeometric function [HyperG2F1](/igorpro/commands/hyperg2f1.md).

### *References* {#references}
Young, L.C., On randomness in ordered sequences, *Annals of Mathematical Statistics*, *12*, 153-162, 1941.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsCMSSDCDF](/igorpro/commands/statscmssdcdf.md), [StatsSRTest](/igorpro/commands/statssrtest.md)